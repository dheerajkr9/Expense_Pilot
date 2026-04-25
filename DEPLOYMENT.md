# ExpensePilot Deployment Guide

Guide for deploying ExpensePilot to production.

## Deployment Architecture

```
┌─────────────────────────────────────┐
│      Frontend (Vercel/Netlify)      │
│   React + Vite (Static Build)       │
└────────────────┬────────────────────┘
                 │
                 ↓ HTTPS
┌─────────────────────────────────────┐
│    Backend (Render/Railway/Heroku)  │
│     Node.js + Express API           │
└────────────────┬────────────────────┘
                 │
                 ↓
┌─────────────────────────────────────┐
│   Database (MongoDB Atlas Cloud)    │
│     Managed MongoDB Service         │
└─────────────────────────────────────┘
```

## Frontend Deployment

### Option 1: Vercel (Recommended)

1. **Push to GitHub**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git push -u origin main
   ```

2. **Deploy on Vercel**
   - Go to [Vercel.com](https://vercel.com)
   - Click "New Project"
   - Import your GitHub repository
   - Select `frontend` folder as root
   - Add environment variables:
     - `VITE_API_URL`: Your backend URL (e.g., https://expensepilot-api.render.com/api)

3. **Configure Domain**
   - Add custom domain in Vercel settings
   - DNS will auto-configure

### Option 2: Netlify

1. **Build frontend**
   ```bash
   cd frontend
   npm run build
   ```

2. **Deploy to Netlify**
   - Drag `frontend/dist` folder to Netlify
   - Or connect GitHub for auto-deploys

3. **Set Environment Variables**
   - Site Settings → Build & Deploy → Environment
   - Add `VITE_API_URL`

### Option 3: GitHub Pages

```bash
cd frontend

# Add to vite.config.js
export default {
  base: '/expensepilot/', // Your repo name
  // ... other config
}

npm run build

# Deploy dist folder to gh-pages branch
```

## Backend Deployment

### Option 1: Render.com (Recommended)

1. **Push to GitHub**
   ```bash
   git push origin main
   ```

2. **Create Render Service**
   - Go to [Render.com](https://render.com)
   - Click "New" → "Web Service"
   - Connect your GitHub repository
   - Configure:
     - **Root Directory**: `backend`
     - **Build Command**: `npm install`
     - **Start Command**: `npm start`

3. **Set Environment Variables**
   - Add in Dashboard → Environment:
     ```
     MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/expensepilot
     NODE_ENV=production
     PORT=5000
     ```

4. **Deploy**
   - Click "Deploy Web Service"
   - Your backend will be live at: `https://expensepilot-api.render.com`

### Option 2: Railway.app

1. **Connect GitHub**
   - Go to [Railway.app](https://railway.app)
   - New Project → Import from GitHub
   - Select your repository

2. **Configure**
   - Select `backend` directory
   - Railway detects Node.js automatically

3. **Add Environment**
   - Go to Variables section
   - Add `MONGODB_URI` and other vars

4. **Deploy**
   - Automatic deployment on git push

### Option 3: Heroku (Using Git)

```bash
# Install Heroku CLI
brew install heroku
# or download from heroku.com

# Login
heroku login

# Create app
heroku create expensepilot-api

# Set buildpack
heroku buildpacks:set heroku/nodejs --app=expensepilot-api

# Add MongoDB Atlas connection
heroku config:set MONGODB_URI="mongodb+srv://..." --app=expensepilot-api

# Deploy backend folder
git push heroku main --subdirectory=backend
```

## Database Setup (MongoDB Atlas)

1. **Create Cluster**
   - Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
   - Create a new project
   - Create a cluster

2. **Create Database User**
   - Database Access → Add Database User
   - Username: `expensepilot_user`
   - Generate secure password
   - Copy password (you won't see it again!)

3. **Get Connection String**
   - Cluster → Connect → Connect your application
   - Copy connection string
   - Replace `<username>`, `<password>`, `<database>` placeholders

4. **Whitelist IPs (if needed)**
   - Network Access → Add IP Address
   - For development: Add your IP
   - For production: Add 0.0.0.0/0 (Render/Railway will work)

5. **Connection String Format**
   ```
   mongodb+srv://expensepilot_user:yourpassword@cluster.mongodb.net/expensepilot?retryWrites=true&w=majority
   ```

## Update Frontend for Production

Edit `frontend/.env.production`:

```
VITE_API_URL=https://your-backend-url.com/api
```

Or set in deployment platform (Vercel, Netlify, etc.)

## Update Backend for Production

Edit `backend/.env` in production:

```
MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/expensepilot
NODE_ENV=production
PORT=5000
```

## Automated CI/CD Pipeline

### GitHub Actions Example

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Deploy Backend
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: cd backend && npm install && npm start

      - name: Deploy Frontend
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: cd frontend && npm install && npm run build
```

## Domain Setup

### Connect Custom Domain

**Frontend (Vercel/Netlify):**
1. Settings → Domains
2. Add your domain
3. Update DNS records (they'll show which ones)
4. SSL certificate auto-generates

**Backend (Render/Railway):**
1. Project Settings → Custom Domain
2. Point CNAME to service URL
3. SSL auto-generates

## Environment Variables Checklist

### Backend Production
- [ ] `MONGODB_URI` - Atlas connection string
- [ ] `NODE_ENV` - Set to `production`
- [ ] `PORT` - Set to `5000`

### Frontend Production
- [ ] `VITE_API_URL` - Your production backend URL

## Performance Tips

### Frontend
- Build is optimized by Vite automatically
- Vercel auto-minifies and compresses
- Use image optimization services

### Backend
- MongoDB Atlas auto-scales
- Render provides auto-scaling on paid plans
- Use monitoring tools to track performance

## Security Checklist

- [ ] MongoDB Atlas IP whitelist configured
- [ ] HTTPS enabled (auto on all platforms)
- [ ] CORS properly configured (backend allows frontend domain)
- [ ] Environment variables not in git
- [ ] Sensitive data in .env files
- [ ] Regular backups enabled (MongoDB Atlas)

## Monitoring & Logs

### View Backend Logs

**Render.com:**
- Dashboard → Logs tab

**Railway:**
- Project → Deployments → Logs

**Heroku:**
```bash
heroku logs --tail --app=expensepilot-api
```

### Monitor Uptime

- [Uptime Robot](https://uptimerobot.com) - Free monitoring
- [StatusPage.io](https://www.statuspage.io)

## Scaling for Production

### Low Traffic (<1000 users/day)
- Vercel free tier for frontend ✓
- Render free tier for backend ✓
- MongoDB Atlas free tier ✓

### Medium Traffic (1000-10000 users/day)
- Vercel Pro for frontend
- Render paid plan for backend
- MongoDB Atlas M10+ cluster

### High Traffic (>10000 users/day)
- Vercel Enterprise
- Render Pro/Enterprise
- MongoDB Atlas dedicated cluster

## Troubleshooting Deployment

### Issue: Frontend can't reach backend

**Solution:**
- Check backend URL in frontend `.env`
- Verify backend is running (`/api/health`)
- Check CORS settings in backend
- Ensure both use HTTPS in production

### Issue: Database connection fails

**Solution:**
- Verify connection string in `.env`
- Check IP whitelist in MongoDB Atlas
- Test connection: `mongosh "connection-string"`
- Verify username/password

### Issue: Slow performance

**Solution:**
- Check MongoDB query performance
- Use MongoDB Atlas monitoring
- Enable caching headers
- Consider upgrading database tier

## Cost Estimate (Monthly)

| Service | Free | Paid |
|---------|------|------|
| Frontend (Vercel) | $0 | $20+ |
| Backend (Render) | $0 (sleeps) | $7+ |
| Database (MongoDB) | $0 (limited) | $57+ |
| **Total** | **~$0** | **~$84+** |

## Production Checklist

Before going live:

- [ ] Frontend deployed and tested
- [ ] Backend deployed and tested
- [ ] Database (MongoDB Atlas) configured
- [ ] Environment variables set in all services
- [ ] Custom domain configured (if using)
- [ ] SSL certificates active
- [ ] CORS properly configured
- [ ] Monitoring set up
- [ ] Backups configured
- [ ] Error tracking (optional: Sentry)
- [ ] Analytics (optional: Google Analytics)

## Next Steps

1. Deploy to staging first
2. Test all features thoroughly
3. Set up monitoring
4. Enable CI/CD pipeline
5. Document deployment process
6. Set up backup strategy
7. Plan scaling strategy

## Support & Help

- [Render Documentation](https://render.com/docs)
- [Vercel Documentation](https://vercel.com/docs)
- [MongoDB Atlas Help](https://docs.atlas.mongodb.com)
- [Railway Docs](https://docs.railway.app)

---

**Ready to deploy?** Start with Render for backend and Vercel for frontend! 🚀
