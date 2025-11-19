# Deployment Guide - Rwanda Crop Recommendation System

Complete guide to deploy the frontend to Render and connect with your backend.

## 📋 Prerequisites

✅ **Backend Already Deployed**
- URL: https://sosens.onrender.com
- Status: Running and accessible
- Endpoints: All 19 endpoints operational

✅ **Git Repository**
- Code pushed to GitHub/GitLab/Bitbucket
- Repository is accessible
- All dependencies listed in package.json

✅ **Render Account**
- Free account at https://render.com
- Credit card optional (free tier available)

## 🚀 Quick Deploy (5 Minutes)

### Step 1: Connect Repository

1. Go to https://dashboard.render.com
2. Click **"New +"** button (top right)
3. Select **"Static Site"**
4. Click **"Connect a repository"**
5. Authorize Render to access your Git provider
6. Select your frontend repository

### Step 2: Configure Build

**Name:** `rwanda-crop-frontend` (or your choice)

**Branch:** `main` (or `master`)

**Build Command:**
```bash
npm install && npm run build
```

**Publish Directory:**
```
dist
```

**Auto-Deploy:** ✅ Yes (deploy on push to main branch)

### Step 3: Deploy

1. Click **"Create Static Site"**
2. Wait for build to complete (2-5 minutes)
3. Build logs will show progress
4. Once complete, you'll get a URL: `https://your-app-name.onrender.com`

### Step 4: Verify Deployment

**Open your deployed site:**
```
https://your-app-name.onrender.com
```

**Should see:**
- Landing page with "Rwanda Crop Recommendation System" header
- "Get Started" button
- "About" and "Login" links
- Clean, responsive design

**Test backend connection in console (F12):**
```javascript
fetch('https://sosens.onrender.com/api/health')
  .then(r => r.json())
  .then(data => console.log('✅ Backend connected:', data))
```

## 🎯 Advanced Configuration

### Using render.yaml (Recommended)

The included `render.yaml` file provides:
- Automatic build configuration
- Security headers
- SPA routing support
- Preview deployments for pull requests

**To use render.yaml:**
1. Ensure `render.yaml` is in repository root
2. Render auto-detects and uses it
3. No manual configuration needed

### Custom Domain (Optional)

**After deployment:**
1. Go to your static site settings
2. Click **"Custom Domain"**
3. Add your domain (e.g., `crops.yoursite.com`)
4. Update DNS records as instructed
5. SSL certificate auto-generated (free)

### Environment Variables

**Not needed!** Backend URL is hardcoded in `/config.ts`:
```typescript
export const API_CONFIG = {
  BASE_URL: "https://sosens.onrender.com/api/",
  TIMEOUT: 30000,
};
```

**If you need to change backend URL:**
1. Edit `/config.ts`
2. Commit and push
3. Render auto-redeploys

## 🔧 Build Configuration

### Vite Configuration

The project uses Vite with this configuration:

**Build Output:** `dist/`  
**Entry Point:** `index.html`  
**Assets:** Bundled with hash in filenames  
**Optimization:** Minified and tree-shaken

### Package.json Scripts

```json
{
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview"
  }
}
```

### Dependencies

All dependencies are production-ready:
- React 18
- TypeScript 5.x
- Tailwind CSS 4.0
- Vite 5.x
- shadcn/ui components
- Lucide icons
- Recharts
- Sonner (toasts)

## 🧪 Post-Deployment Testing

### Test 1: Frontend Loads (30 seconds)

1. Visit your Render URL
2. Should load within 2 seconds
3. No console errors
4. All images/styles load

**Expected:**
```
✅ Page loads
✅ No 404 errors
✅ Tailwind styles applied
✅ Navigation works
```

### Test 2: Backend Connection (1 minute)

**In browser console (F12):**
```javascript
// Test health endpoint
fetch('https://sosens.onrender.com/api/health')
  .then(r => r.json())
  .then(data => {
    if (data.status === 'healthy') {
      console.log('✅ Backend connected');
    } else {
      console.error('❌ Backend unhealthy');
    }
  })
  .catch(e => console.error('❌ Backend unreachable:', e));
```

**Expected:**
```json
{
  "status": "healthy",
  "timestamp": "2025-11-19T10:30:00"
}
```

### Test 3: User Registration (2 minutes)

1. Click **"Get Started"** or go to register page
2. Fill form:
   - Full Name: `Test Farmer`
   - Phone: `+250788123456`
   - Email: `test@farmer.com`
   - Password: `test123456`
3. Click **"Register"**

**Expected:**
- ✅ Success toast appears
- ✅ Redirects to dashboard
- ✅ User logged in

**If fails:**
- Check browser console for errors
- Verify backend is running
- Check network tab for API errors

### Test 4: Login (1 minute)

1. Go to login page
2. Enter registered credentials
3. Click **"Sign In"**

**Expected:**
- ✅ Success toast: "Login successful"
- ✅ Redirects to dashboard
- ✅ Token saved in localStorage

**Verify in console:**
```javascript
localStorage.getItem('sosens_auth_token') // Should show JWT token
JSON.parse(localStorage.getItem('sosens_user')) // Should show user data
```

### Test 5: Forgot Password (3 minutes)

1. Click **"Forgot password?"** on login page
2. Enter email/phone
3. Click **"Send Reset Link"**

**Expected:**
- ✅ Success toast appears
- ✅ Dialog shows step 2
- ✅ If backend DEBUG=True, token displays

**Complete reset:**
1. Enter token (from debug or email/SMS)
2. Enter new password
3. Confirm password
4. Click **"Reset Password"**
5. Success toast appears
6. Dialog closes
7. Login with new password

### Test 6: Crop Prediction (2 minutes)

1. Login as farmer
2. Navigate to prediction page
3. Enter soil data:
   - pH: 6.5
   - Nitrogen: 50
   - Phosphorus: 25
   - Potassium: 200
   - Zinc: 5
   - Sulfur: 15
4. Check "Include weather data" (optional)
5. Click **"Get Recommendation"**

**Expected:**
- ✅ Loading state shows
- ✅ Prediction appears (2-5 seconds)
- ✅ Shows crop name
- ✅ Shows confidence percentage
- ✅ Shows soil health status
- ✅ Shows fertilizer advice
- ✅ Shows alternative crops

### Test 7: View History (1 minute)

1. Stay on dashboard
2. Scroll to "Recent Predictions" section
3. Should see your prediction

**Expected:**
- ✅ Prediction listed with date
- ✅ Shows crop recommended
- ✅ Shows confidence
- ✅ Can click to view details

### Test 8: Admin Features (3 minutes)

**Note:** Only if you have admin user

1. Login with admin credentials
2. Should see "Admin Dashboard" option
3. Click to view admin panel

**Expected features:**
- ✅ System analytics
- ✅ User list
- ✅ Send notifications
- ✅ Broadcast messages

## 🔒 Security Checklist

After deployment, verify:

- [x] HTTPS enabled (Render auto-provides)
- [x] Security headers set (from render.yaml)
- [x] JWT tokens stored in localStorage only
- [x] No API keys in frontend code
- [x] Backend validates all requests
- [x] CORS enabled on backend for your domain

## 📊 Performance Optimization

### Already Optimized

✅ **Code Splitting:** Vite automatically splits vendor code  
✅ **Minification:** JavaScript and CSS minified  
✅ **Tree Shaking:** Unused code removed  
✅ **Asset Hashing:** Cache-friendly filenames  
✅ **Gzip Compression:** Render auto-enables  

### Performance Metrics

**Target metrics:**
- First Contentful Paint: < 1.5s
- Time to Interactive: < 3s
- Lighthouse Score: > 90

**Measure after deployment:**
1. Open Chrome DevTools
2. Go to "Lighthouse" tab
3. Click "Generate report"
4. Review performance score

## 🔄 Continuous Deployment

### Auto-Deploy on Push

Render automatically redeploys when you push to main branch:

```bash
# Make changes locally
git add .
git commit -m "Update feature"
git push origin main

# Render auto-detects push and rebuilds (2-5 minutes)
```

### Deploy Logs

**View build logs:**
1. Go to Render dashboard
2. Click your static site
3. Click **"Logs"** tab
4. See real-time build progress

**Common build errors:**
```
❌ "Module not found" → Missing dependency, run npm install
❌ "Build failed" → Check TypeScript errors
❌ "Out of memory" → Increase build instance (paid plans)
```

### Preview Deployments

**For pull requests:**
1. Create PR in your repository
2. Render automatically deploys preview
3. Get unique URL for testing
4. Merge PR to deploy to production

## 🐛 Troubleshooting

### Issue: Build Fails

**Error:** `npm ERR! missing script: build`

**Solution:**
Ensure `package.json` has:
```json
{
  "scripts": {
    "build": "tsc && vite build"
  }
}
```

---

**Error:** `Module not found: Can't resolve 'xyz'`

**Solution:**
```bash
# Ensure dependency in package.json
npm install xyz
git add package.json package-lock.json
git commit -m "Add missing dependency"
git push
```

---

**Error:** `Out of memory`

**Solution:**
- Use Render paid plan (more memory)
- Or reduce bundle size
- Or optimize dependencies

### Issue: Site Loads But Shows Blank Page

**Cause:** Routing issue or JavaScript error

**Solution:**
1. Check browser console for errors
2. Verify `dist/index.html` exists
3. Check `render.yaml` routing config
4. Ensure Vite build completed successfully

### Issue: 404 on Page Refresh

**Cause:** SPA routing not configured

**Solution:**
Ensure `render.yaml` has:
```yaml
routes:
  - type: rewrite
    source: /*
    destination: /index.html
```

### Issue: Backend Connection Fails

**Error:** `Failed to fetch` or `Network error`

**Solution:**
1. Check backend is running:
   ```bash
   curl https://sosens.onrender.com/api/health
   ```
2. Verify CORS enabled on backend
3. Check backend URL in `/config.ts`
4. Wait for backend cold start (30-60 seconds)

### Issue: Login Works Locally But Not on Render

**Cause:** CORS or backend configuration

**Solution:**
1. Verify backend CORS allows your Render domain
2. Check backend logs for errors
3. Ensure JWT secret is set on backend
4. Verify database is accessible

### Issue: Images Not Loading

**Cause:** Asset path issue

**Solution:**
1. Check image paths are relative
2. Verify images in `/public` directory
3. Use Vite asset imports:
   ```typescript
   import logo from './assets/logo.png'
   ```

## 📱 Mobile Testing

After deployment, test on mobile:

**iOS:**
- Safari (iPhone/iPad)
- Chrome (iPhone/iPad)

**Android:**
- Chrome (Android)
- Firefox (Android)

**Test features:**
- ✅ Responsive layout
- ✅ Touch interactions
- ✅ Form inputs
- ✅ Navigation
- ✅ API calls

## 🌐 Custom Domain Setup (Optional)

### Add Custom Domain

1. Go to Render dashboard
2. Select your static site
3. Click **"Settings"**
4. Scroll to **"Custom Domain"**
5. Click **"Add Custom Domain"**
6. Enter: `crops.yourdomain.com`

### Configure DNS

**Add CNAME record:**
```
Type: CNAME
Name: crops (or your subdomain)
Value: your-app-name.onrender.com
TTL: 3600 (or auto)
```

### SSL Certificate

- Render auto-provisions SSL (Let's Encrypt)
- Takes 5-10 minutes after DNS propagation
- HTTPS automatically enforced

## 📈 Monitoring

### Render Dashboard

**Monitor:**
- Build status
- Deploy history
- Bandwidth usage
- Response times

### Browser Monitoring

**In production, monitor:**
- Console errors (use error tracking service)
- API response times
- User flows
- Conversion rates

### Recommended Tools

- **Sentry** - Error tracking
- **Google Analytics** - User analytics
- **Hotjar** - User behavior
- **LogRocket** - Session replay

## 🔄 Rollback

### Revert to Previous Deployment

1. Go to Render dashboard
2. Select your static site
3. Click **"Deploys"** tab
4. Find previous successful deploy
5. Click **"Redeploy"**

### Manual Rollback

```bash
# Revert last commit
git revert HEAD
git push origin main

# Or reset to specific commit
git reset --hard <commit-hash>
git push --force origin main
```

## ✅ Production Checklist

Before going live:

**Configuration:**
- [x] Backend URL correct in `/config.ts`
- [x] All dependencies in `package.json`
- [x] `render.yaml` configured
- [x] Repository pushed to Git

**Testing:**
- [x] Registration works
- [x] Login works
- [x] Forgot password works
- [x] Predictions work
- [x] History loads
- [x] Admin features work (if applicable)

**Performance:**
- [x] Lighthouse score > 90
- [x] Page loads < 2 seconds
- [x] API calls < 5 seconds
- [x] Mobile responsive

**Security:**
- [x] HTTPS enabled
- [x] Security headers set
- [x] No sensitive data in frontend
- [x] JWT validation on backend

**Monitoring:**
- [ ] Error tracking setup (optional)
- [ ] Analytics configured (optional)
- [ ] Uptime monitoring (optional)

## 🎉 You're Live!

Once deployed successfully:

1. ✅ Frontend is live at: `https://your-app-name.onrender.com`
2. ✅ Connected to backend: `https://sosens.onrender.com`
3. ✅ All features operational
4. ✅ Auto-deploys on Git push
5. ✅ Free SSL certificate
6. ✅ CDN enabled

**Share with users:**
```
🌾 Rwanda Crop Recommendation System
🔗 https://your-app-name.onrender.com

Features:
✅ User registration & login
✅ Forgot password
✅ Crop predictions
✅ Prediction history
✅ Admin dashboard
```

---

**Last Updated:** November 19, 2025  
**Status:** Production Ready  
**Deployment Platform:** Render  
**Backend:** https://sosens.onrender.com
