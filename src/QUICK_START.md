# Quick Start Guide

Get the Rwanda Crop Recommendation System running in 5 minutes.

## 🚀 Deploy to Render (5 Minutes)

### One-Command Deploy

```bash
# 1. Push code to Git
git add .
git commit -m "Ready for deployment"
git push origin main

# 2. Deploy on Render
# → Go to https://dashboard.render.com
# → Click "New +" → "Static Site"
# → Connect repository
# → Build: npm install && npm run build
# → Publish: dist
# → Click "Create Static Site"
```

**That's it!** Your app will be live in 3-5 minutes.

## 🧪 Quick Test (2 Minutes)

### 1. Check Backend Connection
```javascript
// In browser console (F12)
fetch('https://sosens.onrender.com/api/health')
  .then(r => r.json())
  .then(console.log)

// Expected: { status: "healthy" }
```

### 2. Test Registration
```
1. Click "Get Started"
2. Fill form:
   - Name: Test Farmer
   - Phone: +250788123456
   - Email: test@farmer.com
   - Password: test123
3. Click "Register"
4. Should see success ✅
```

### 3. Test Prediction
```
1. Login
2. Go to prediction page
3. Enter: pH=6.5, N=50, P=25, K=200, Zn=5, S=15
4. Click "Get Recommendation"
5. Should see crop recommendation ✅
```

## 📁 Project Structure

```
/
├── components/        # React components
│   ├── ui/           # shadcn/ui library
│   ├── HomePage.tsx
│   ├── LoginPage.tsx (with forgot password)
│   ├── RegisterPage.tsx
│   ├── DashboardPage.tsx
│   ├── FarmerDashboard.tsx
│   ├── AdminDashboard.tsx
│   └── PredictPage.tsx
├── lib/
│   ├── api.ts        # All 19 API endpoints
│   └── auth.ts       # Authentication logic
├── styles/
│   └── globals.css   # Tailwind styles
├── App.tsx           # Main app
├── config.ts         # Backend URL
├── render.yaml       # Render config
├── README.md         # Full documentation
└── DEPLOY.md         # Deployment guide
```

## 🔗 Important URLs

- **Backend API:** https://sosens.onrender.com/api/
- **API Docs:** https://sosens.onrender.com/docs
- **Health Check:** https://sosens.onrender.com/api/health

## 🛠️ Local Development

```bash
# Install
npm install

# Run locally
npm run dev

# Build for production
npm run build

# Preview build
npm run preview
```

## 🔌 API Endpoints (19 Total)

### Authentication (5)
```
POST /api/auth/register
POST /api/auth/login
GET  /api/auth/me
POST /api/auth/forgot-password
POST /api/auth/reset-password
```

### Predictions (5)
```
POST /api/predict
GET  /api/recommendations
GET  /api/recommendations/{id}
POST /api/soil-readings
GET  /api/soil-readings
```

### Other (9)
```
POST /api/weather
GET  /api/preferences
PUT  /api/preferences
GET  /api/admin/analytics
GET  /api/admin/users
POST /api/admin/weather-notification
POST /api/admin/broadcast
POST /api/admin/bulk-predict
GET  /api/admin/notifications
```

## 🎯 Key Features

✅ User registration & login  
✅ Forgot password with token reset  
✅ ML-powered crop predictions  
✅ Soil analysis  
✅ Weather integration  
✅ Prediction history  
✅ Admin dashboard  
✅ SMS/Email notifications  
✅ Responsive design  

## 🔒 Environment

**Backend URL:** Configured in `/config.ts`
```typescript
export const API_CONFIG = {
  BASE_URL: "https://sosens.onrender.com/api/",
  TIMEOUT: 30000,
};
```

**No environment variables needed!**

## 🐛 Quick Troubleshooting

### Backend not responding?
```bash
# Check health
curl https://sosens.onrender.com/api/health

# Wait 30-60 seconds for cold start (free tier)
```

### Login not working?
```javascript
// Check token in console
localStorage.getItem('sosens_auth_token')
```

### Build failing on Render?
```
1. Check build command: npm install && npm run build
2. Check publish directory: dist
3. View build logs for specific error
```

## 📞 Support

- **README.md** - Complete documentation
- **DEPLOY.md** - Deployment guide
- **render.yaml** - Auto-configuration

## ✅ Production Ready

This application is **100% ready** to deploy:
- ✅ All features implemented
- ✅ Connected to production backend
- ✅ No mock data or fallbacks
- ✅ Fully tested and documented
- ✅ Optimized for performance
- ✅ Mobile responsive
- ✅ Secure authentication

**Deploy now and it will work immediately!**

---

**Version:** 2.0.0  
**Last Updated:** November 19, 2025
