# Cloudflare Pages Deployment Guide

## Overview

Your QuantTrade Next.js application is now configured for Cloudflare Pages deployment using static export mode.

## Configuration Summary

### Files Modified/Created

1. **next.config.ts** - Configured for static export
   ```typescript
   output: 'export'
   images: { unoptimized: true }
   ```

2. **wrangler.toml** - Cloudflare Pages configuration
   ```toml
   name = "quanttrade-co-id"
   compatibility_date = "2024-01-01"
   pages_build_output_dir = "./out"
   ```

3. **package.json** - Added deployment scripts
   - `pages:build` - Build static export
   - `pages:deploy` - Deploy to Cloudflare Pages
   - `pages:dev` - Local preview with Wrangler

4. **.gitignore** - Added Wrangler directories

## Deployment Commands

### Build Locally
```bash
npm run pages:build
```
This creates a static export in the `./out` directory.

### Deploy to Cloudflare Pages

#### First-time Setup
```bash
# Login to Cloudflare (if not already logged in)
npx wrangler login

# Deploy
npm run pages:deploy
```

#### Subsequent Deployments
```bash
npm run pages:deploy
```

### Local Preview (Optional)
```bash
# First build the site
npm run pages:build

# Then preview locally
npm run pages:dev
```

## Custom Domain Setup

After deployment, configure your custom domain in Cloudflare Dashboard:

1. Go to **Workers & Pages** → **quanttrade-co-id**
2. Click **Custom domains** tab
3. Add `quanttrade.co.id` and `www.quanttrade.co.id`
4. Follow DNS configuration instructions

## Environment Variables

Currently, no environment variables are required. If you add API integrations in the future:

1. Go to Cloudflare Dashboard → **Workers & Pages** → **quanttrade-co-id**
2. Navigate to **Settings** → **Environment variables**
3. Add variables for Production and Preview environments

## Continuous Deployment (Optional)

To enable automatic deployments from GitHub:

1. In Cloudflare Dashboard, go to **Workers & Pages**
2. Click **Create application** → **Pages** → **Connect to Git**
3. Select your `quanttrade.co.id` repository
4. Configure build settings:
   - **Build command**: `npm run pages:build`
   - **Build output directory**: `out`
   - **Root directory**: `/`

## Troubleshooting

### Build fails
- Ensure all dependencies are installed: `npm install`
- Check that `next.config.ts` has `output: 'export'`

### Deployment fails
- Verify you're logged in: `npx wrangler whoami`
- Check `wrangler.toml` configuration
- Ensure `./out` directory exists after build

### Site not loading
- Verify deployment completed successfully
- Check Cloudflare Pages dashboard for deployment logs
- Ensure DNS is properly configured for custom domain

## Next Steps

1. ✅ Configuration complete
2. Run `npm run pages:deploy` to deploy to Cloudflare Pages
3. Configure custom domain in Cloudflare Dashboard
4. (Optional) Set up GitHub integration for continuous deployment
