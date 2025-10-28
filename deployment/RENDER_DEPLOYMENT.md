# Deploy Food Expiry Tracker to Render

## 🚀 Step-by-Step Render Deployment Guide

### Prerequisites
- GitHub account
- Render account (sign up at https://render.com - FREE)
- Google Gemini API key (for AI features)

---

## Step 1: Push Code to GitHub

1. **Create a new GitHub repository**
   - Go to https://github.com/new
   - Name it: `food-expiry-tracker`
   - Keep it public or private

2. **Upload deployment folder contents**
   
   **Option A - Upload only deployment contents (Recommended):**
   - Copy all files from INSIDE the `deployment` folder
   - Push to repository root
   - Leave "Root Directory" blank in Render
   
   **Option B - Upload whole project:**
   - Push the entire parent folder (including deployment folder)
   - Set "Root Directory" to `deployment` in Render

---

## Step 2: Deploy on Render

### A. Create New Web Service

1. Go to https://dashboard.render.com
2. Click **"New +"** → **"Web Service"**
3. Connect your GitHub repository
4. Select `food-expiry-tracker` repository

### B. Configure Web Service

Fill in these settings:

| Setting | Value |
|---------|-------|
| **Name** | food-expiry-tracker |
| **Runtime** | Python 3 |
| **Root Directory** | `deployment` (if you pushed the whole folder) OR leave blank (if you pushed only deployment contents) |
| **Build Command** | `pip install -r requirements.txt` |
| **Start Command** | `gunicorn app_sqlite:app` |
| **Instance Type** | Free |

### C. Add Environment Variables

Click **"Advanced"** and add these environment variables:

```
SECRET_KEY = <click Generate> or use any random string
GEMINI_API_KEY = your_gemini_api_key_here
PYTHON_VERSION = 3.10.0
```

**Optional (for email notifications):**
```
SMTP_EMAIL = your_email@gmail.com
SMTP_PASSWORD = your_gmail_app_password
```

### D. Deploy

1. Click **"Create Web Service"**
2. Wait 5-10 minutes for deployment
3. Your app will be live at: `https://food-expiry-tracker.onrender.com`

---

## Step 3: Get Google Gemini API Key

1. Go to https://makersuite.google.com/app/apikey
2. Click **"Create API Key"**
3. Copy the key
4. Add it to Render environment variables:
   - Go to your service → **Environment**
   - Add `GEMINI_API_KEY` = your_key

---

## Important Notes

### Database
- Using **SQLite** (file-based database)
- Data persists on Render's free tier
- For production, consider upgrading to PostgreSQL

### File Uploads
- Images upload to `static/uploads/`
- Free tier has limited disk space
- Consider using cloud storage (Cloudinary, AWS S3) for production

### Free Tier Limitations
- Spins down after 15 minutes of inactivity
- First load after inactivity takes ~30 seconds
- 750 hours/month free (enough for 24/7 usage)

---

## Troubleshooting

### Build Failed?
- Check build logs in Render dashboard
- Ensure all dependencies in requirements.txt
- Try changing Python version to 3.11.0

### App Not Loading?
- Check application logs
- Verify environment variables are set
- Ensure start command is: `gunicorn app_sqlite:app`

### OCR Not Working?
- Tesseract may not work on free tier
- Consider disabling OCR or upgrading instance

---

## Upgrade to MySQL (Optional)

If you want to use MySQL instead of SQLite:

1. **Create MySQL Database** (Render doesn't offer free MySQL)
   - Use external service like PlanetScale (free tier)
   - Or upgrade Render instance

2. **Update app configuration**
   - Rename `app.py` (MySQL version) 
   - Update start command to: `gunicorn app:app`
   - Add database credentials to environment variables

---

## Monitoring & Maintenance

- **View Logs**: Render Dashboard → Your Service → Logs
- **Check Status**: Dashboard shows deployment status
- **Auto-Deploy**: Enabled by default when you push to GitHub
- **Custom Domain**: Available on paid plans

---

## Cost

- **Free Tier**: $0/month
  - 750 hours/month
  - Spins down after inactivity
  - Limited resources

- **Paid Tier**: $7/month
  - Always on
  - More resources
  - Custom domains

---

## Next Steps After Deployment

1. ✅ Test all features (login, dashboard, OCR, recipes)
2. ✅ Create your first user account
3. ✅ Add some food items
4. ✅ Test AI chatbot with Gemini API
5. 🎉 Share your app URL!

---

## Support Links

- Render Docs: https://render.com/docs
- Render Community: https://community.render.com
- Python on Render: https://render.com/docs/deploy-flask

---

**Your app will be live at:**
`https://your-app-name.onrender.com`

Good luck! 🚀
