# Frontend Deployment Guide

## Common Deployment Issues & Solutions

### 1. Environment Variables
Make sure to set the correct backend URL in your deployment platform:

**For Vercel:**
- Go to Project Settings → Environment Variables
- Add `VITE_BACKEND_URL` with your backend URL (e.g., `https://your-app.herokuapp.com`)

**For Netlify:**
- Go to Site Settings → Environment Variables
- Add `VITE_BACKEND_URL` with your backend URL

**For Heroku:**
- Use `heroku config:set VITE_BACKEND_URL=https://your-backend-url.herokuapp.com`

### 2. Build Configuration
The Vite config has been optimized for deployment:
- Base path set to `/` for root deployment
- Proper asset handling
- Disabled sourcemaps for production

### 3. CORS Issues
If you're getting CORS errors, make sure your backend allows your frontend domain:

```javascript
// In your backend app.js
app.use(cors({
  origin: ['http://localhost:3000', 'https://your-frontend-domain.vercel.app'],
  credentials: true
}));
```

### 4. Routing Issues
For SPA routing, make sure your deployment platform redirects all routes to `index.html`:
- **Vercel**: Uses `vercel.json` (already configured)
- **Netlify**: Uses `netlify.toml` and `_redirects` (already configured)

### 5. Build Commands
Make sure your deployment platform uses the correct build command:
- Build command: `npm run build`
- Publish directory: `dist`

## Platform-Specific Instructions

### Vercel
1. Connect your GitHub repository
2. Set build command to `cd frontend && npm run build`
3. Set output directory to `frontend/dist`
4. Add environment variable `VITE_BACKEND_URL`

### Netlify
1. Connect your GitHub repository
2. Set build command to `cd frontend && npm install && npm run build`
3. Set publish directory to `frontend/dist`
4. Add environment variable `VITE_BACKEND_URL`

### Heroku
1. Create a `package.json` in the root with:
```json
{
  "scripts": {
    "build": "cd frontend && npm install && npm run build",
    "start": "cd frontend && npm run serve"
  }
}
```
2. Add `VITE_BACKEND_URL` to config vars

## Troubleshooting

### Build Fails
- Check Node.js version (should be 18.x or higher)
- Clear `node_modules` and reinstall: `rm -rf node_modules && npm install`
- Check for TypeScript errors if using TypeScript

### Runtime Errors
- Check browser console for specific errors
- Verify environment variables are set correctly
- Check network tab for failed API calls

### 404 on Refresh
- Ensure SPA routing is configured (redirects to index.html)
- Check that all routes are properly handled

## Testing Locally
```bash
cd frontend
npm run build
npm run preview
```

This will serve the production build locally for testing.
