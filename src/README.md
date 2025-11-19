# SoSens Frontend

Modern web application providing smart crop recommendations to Rwandan farmers based on soil and weather data analysis.

## Overview

React TypeScript application that connects to a FastAPI backend for:
- Intelligent crop recommendations based on soil properties
- Weather-integrated predictions
- User authentication and authorization
- Prediction history tracking
- Admin analytics dashboard
- SMS/Email notifications

Backend: https://sosens.onrender.com

## Features

### For Farmers
- User registration and login (phone/email)
- Password reset with token-based verification
- Crop predictions based on soil data (pH, N, P, K, Zn, S)
- Prediction history and soil readings tracking
- Weather data integration
- Notification preferences management

### For Admins
- User management and statistics
- System analytics dashboard
- Weather notifications broadcast
- Bulk messaging system
- Bulk prediction processing
- Notification log tracking

## Tech Stack

React 18 + TypeScript | Tailwind CSS | shadcn/ui | Lucide React | Recharts | Fetch API | JWT Authentication

## Project Structure

```
/
├── components/
│   ├── ui/                    # UI components
│   ├── HomePage.tsx
│   ├── LoginPage.tsx
│   ├── RegisterPage.tsx
│   ├── DashboardPage.tsx
│   ├── FarmerDashboard.tsx
│   ├── AdminDashboard.tsx
│   ├── PredictPage.tsx
│   └── Navigation.tsx
├── lib/
│   ├── api.ts                 # 19 API endpoints
│   └── auth.ts
├── styles/
│   └── globals.css
├── App.tsx
└── config.ts
```

## Local Development

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Open http://localhost:5173
```

## API Endpoints (19 Total)

**Authentication**: Register, Login, Get User, Forgot Password, Reset Password  
**Predictions**: Get Recommendation, History, Get Specific  
**Soil**: Submit Reading, Get History  
**Weather**: Get Weather Data  
**Preferences**: Get/Update User Preferences  
**Admin**: Analytics, Users, Weather Notifications, Broadcast, Bulk Predict, Logs  
**System**: Health Check

Full API documentation: https://sosens.onrender.com/docs

## Deployment on Render

### Step 1: Create Static Site
1. Go to https://dashboard.render.com/
2. Click "New +" → "Static Site"
3. Connect your Git repository

### Step 2: Build Configuration
**Build Command:**
```bash
npm install && npm run build
```

**Publish Directory:**
```
dist
```

### Step 3: Deploy
1. Click "Create Static Site"
2. Wait for build (2-5 minutes)
3. Access at: https://your-app-name.onrender.com

No environment variables needed - backend URL is configured in `/config.ts`

## Verify Deployment

Open browser console (F12) and run:
```javascript
fetch('https://sosens.onrender.com/api/health')
  .then(r => r.json())
  .then(data => console.log('Backend status:', data))
```

Expected response:
```json
{
  "status": "healthy",
  "timestamp": "2025-11-19T10:30:00"
}
```

## Testing

### Test Registration
1. Go to registration page
2. Enter: Full Name, Phone (+250788123456), Email, Password
3. Click "Register"
4. Should receive success message

### Test Login
1. Use registered credentials
2. Click "Sign In"
3. Should redirect to dashboard

### Test Prediction
1. Login as farmer
2. Navigate to prediction page
3. Enter soil data (pH: 6.5, N: 50, P: 25, K: 200, Zn: 5, S: 15)
4. Click "Get Recommendation"
5. Should receive crop prediction

### Test Admin
1. Login with admin credentials
2. Access admin dashboard
3. View analytics and user list
4. Test notification sending

## Troubleshooting

**Network Error**: Backend may be sleeping (Render free tier). Wait 30-60 seconds for cold start.

**Login Fails**: Try registering a new account or check backend status.

**Predictions Always Same Crop**: Check backend logs for ML model errors.

**Token Expired**: Logout and login again to get new token.

## Test Endpoints (Browser Console)

**Backend Health:**
```javascript
fetch('https://sosens.onrender.com/api/health')
  .then(r => r.json())
  .then(console.log)
```

**Check Authentication:**
```javascript
localStorage.getItem('sosens_auth_token')
JSON.parse(localStorage.getItem('sosens_user'))
```

**Test Prediction:**
```javascript
const token = localStorage.getItem('sosens_auth_token');
fetch('https://sosens.onrender.com/api/predict', {
  method: 'POST',
  headers: {
    'Authorization': `Bearer ${token}`,
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    ph: 6.5, nitrogen: 50, phosphorus: 25, potassium: 200, zinc: 5, sulfur: 15
  })
})
.then(r => r.json())
.then(console.log)
```

## Performance

- Initial load: 1-2 seconds
- Login/Register: 1-3 seconds
- Prediction: 2-5 seconds
- Render cold start: 30-60 seconds (after 15 min inactivity)

## Browser Support

Chrome 90+, Firefox 88+, Safari 14+, Edge 90+

## Update Process

```bash
git add .
git commit -m "Update description"
git push origin main
# Render auto-deploys (wait 2-5 minutes)
```

## Security

- JWT token-based authentication
- Secure password hashing (backend)
- Token expiration handling
- Protected admin routes
- Input validation
- XSS prevention

## Responsive Design

Works on Desktop (1024px+), Tablet (768px-1023px), Mobile (320px-767px)

## License

Private project for Rwanda agricultural system

## Screenshots

### Login Page
![Login](frontend/assets/screenshots/login.png)

### Registration
![Register](frontend/assets/screenshots/register.png)

### Dashboard
![Dashboard](frontend/assets/screenshots/dashboard.png)

### Soil Analysis
![Soil Analysis](frontend/assets/screenshots/soil-analysis.png)

### Crop Recommendation
![Recommendation](frontend/assets/screenshots/recommendation.png)

### Weather Integration
![Weather](frontend/assets/screenshots/weather.png)

### Admin Panel
![Admin](frontend/assets/screenshots/admin-dashboard.png)

## Status

Production Ready | Version 2.0.0 | Last Updated: November 2025

