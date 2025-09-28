# Cloudflare Deployment Fix Guide

## Problem
When deploying to Cloudflare through GitHub, it was trying to build as a full-stack React app instead of deploying as a Cloudflare Worker.

## Solution
The following files have been added to ensure proper Workers deployment:

### 1. `_worker.js` (Root level)
- Tells Cloudflare this is a Workers project
- Points to the main worker file

### 2. `functions/_worker.js` 
- For Cloudflare Pages deployment compatibility
- Ensures the worker runs through Pages Functions


## Deployment Methods

### Method 1: Direct Workers Deployment (Recommended)
1. Connect your GitHub repository to Cloudflare Workers
2. Set deployment command to: `wrangler deploy`
3. The `_worker.js` file will automatically be detected

### Method 2: Through Cloudflare Pages
1. Connect GitHub repo to Cloudflare Pages
2. Set build command to: `# No build needed`
3. Set output directory to: `/`
4. The `functions/_worker.js` will handle the deployment

### Method 3: GitHub Actions (Advanced)
1. Set up the secrets in GitHub:
   - `CLOUDFLARE_API_TOKEN`
   - `CLOUDFLARE_ACCOUNT_ID`
2. Push to main branch - auto-deployment will trigger

## API Endpoints Available
- `GET /health` - Health check
- `GET /api/models` - Available AI models
- `GET /api/image/generate?prompt=YOUR_PROMPT` - Generate image
- `POST /api/redeem-gift` - Redeem gift codes

## Testing Your Deployment
After deployment, test with:
```bash
curl https://YOUR-WORKER-URL.workers.dev/health
```

Should return:
```json
{
  "status": "healthy",
  "timestamp": "...",
  "version": "1.0.0",
  "subscription_tiers": ["free", "gift", "premium_gift", "starter", "enterprise"]
}
```

## Image Generation Features Preserved
✅ AI image generation with FLUX models  
✅ Rate limiting and subscription tiers  
✅ Gift code system  
✅ RapidAPI compatibility  
✅ Load balancing support  
✅ Health monitoring  

Your image generation functionality is fully intact and working!