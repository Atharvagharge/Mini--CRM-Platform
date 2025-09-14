# Vercel Deployment Guide

## Quick Steps to Deploy Frontend on Vercel

### 1. Push Changes to GitHub
```bash
git add .
git commit -m "Add Vercel deployment configuration"
git push origin main
```

### 2. Deploy on Vercel

**Option A: Using Vercel CLI (Recommended)**
```bash
# Install Vercel CLI globally
npm i -g vercel

# Login to Vercel
vercel login

# Deploy from frontend directory
cd frontend
vercel

# Follow the prompts:
# - Set up and deploy? Yes
# - Which scope? (your account)
# - Link to existing project? No
# - Project name: mini-crm-frontend
# - Directory: ./
# - Override settings? No
```

**Option B: Using Vercel Dashboard**
1. Go to [vercel.com](https://vercel.com)
2. Click "New Project"
3. Import your GitHub repository
4. Set these settings:
   - **Framework Preset**: Vite
   - **Root Directory**: `frontend`
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
   - **Install Command**: `npm install`

### 3. Set Environment Variables
In Vercel Dashboard → Project Settings → Environment Variables:
- `VITE_BACKEND_URL` = `https://mini-crm-backend-r2uj.onrender.com`

### 4. Update Backend CORS (Already Done)
Your backend now allows Vercel domains. If you need to add more domains later, update the CORS configuration in `backend/src/app.js`.

### 5. Test Your Deployment
1. Visit your Vercel URL (e.g., `https://mini-crm-frontend.vercel.app`)
2. Check browser console for any errors
3. Test login functionality
4. Test API calls

## Troubleshooting

### Common Issues:
1. **CORS Errors**: Make sure backend CORS includes your Vercel domain
2. **404 on Refresh**: Vercel handles SPA routing automatically with the `vercel.json` config
3. **API Calls Failing**: Check that `VITE_BACKEND_URL` is set correctly
4. **Build Fails**: Make sure you're in the `frontend` directory when running `vercel`

### If Build Fails:
```bash
cd frontend
npm install
npm run build
# If this works locally, the issue is with Vercel settings
```

### Environment Variables:
Make sure these are set in Vercel:
- `VITE_BACKEND_URL` = `https://mini-crm-backend-r2uj.onrender.com`

## Your URLs:
- **Frontend**: `https://mini-crm-frontend.vercel.app` (after deployment)
- **Backend**: `https://mini-crm-backend-r2uj.onrender.com` (already deployed)
