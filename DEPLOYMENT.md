# Deployment Guide - Chatsphere

## Deployment to Render.com

This guide walks you through deploying the Chatsphere application to Render.

### Prerequisites

- GitHub account with repository pushed
- Render.com account
- MongoDB Atlas account (or any MongoDB instance)

### Step 1: Prepare Your Repository

Ensure all files are committed and pushed to GitHub:

```bash
git add .
git commit -m "Prepare for deployment"
git push origin main
```

### Step 2: Create Render Account

1. Go to [render.com](https://render.com)
2. Sign up with your GitHub account
3. Give Render permission to access your repositories

### Step 3: Create Web Service on Render

1. Go to Dashboard → Click "New +"
2. Select "Web Service"
3. Connect your `chatsphere` repository
4. Fill in the following details:

| Field | Value |
|-------|-------|
| Name | `chatsphere` |
| Environment | `Node` |
| Region | Select closest to your users |
| Branch | `main` |
| Build Command | `npm install && npm install --include=dev --prefix frontend && npm run build --prefix frontend` |
| Start Command | `node backend/index.js` |

### Step 4: Add Environment Variables

In the Render dashboard, go to **Environment** section and add:

```
PORT=3000
MONGODB_CONNECT=<your_mongodb_atlas_connection_string>
JWT_SECRET=<generate_a_strong_random_string>
SECURE=production
NODE_ENV=production
```

**How to generate a strong JWT_SECRET:**

Use this PowerShell command:
```powershell
-join ((1..32) | ForEach-Object { [char][int]((48..122) | Get-Random) })
```

Or this Bash command:
```bash
openssl rand -hex 32
```

### Step 5: Configure MongoDB

1. Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a cluster (free tier available)
3. Get your connection string: `mongodb+srv://username:password@cluster.mongodb.net/database?retryWrites=true&w=majority`
4. Add your Render IP to MongoDB whitelist:
   - Go to Network Access → Add IP Address
   - Add `0.0.0.0/0` for Render (or add Render's IP when known)

### Step 6: Deploy

1. Click the "Create Web Service" button
2. Render will automatically deploy when you push to the main branch
3. Monitor the deployment in the **Logs** tab
4. Once status shows "Live", your app is deployed!

### Step 7: Test Your Deployment

1. Visit your app at `https://<your-service-name>.onrender.com`
2. Register a new account
3. Test messaging between multiple browsers

### Environment Variables Reference

| Variable | Description | Example |
|----------|---|---|
| `MONGODB_CONNECT` | MongoDB connection string | `mongodb+srv://user:pass@cluster.mongodb.net/db` |
| `JWT_SECRET` | Secret key for JWT tokens | `abc123xyz789...` |
| `PORT` | Server port (Render sets this) | `3000` |
| `NODE_ENV` | Environment mode | `production` |
| `SECURE` | Security mode | `production` |

### Troubleshooting

#### Issue: Application shows blank page
**Solution:**
- Check browser DevTools Console for errors
- Check Render logs in Dashboard → Logs
- Verify all environment variables are set correctly

#### Issue: Socket.io connection fails
**Solution:**
- Check Render logs for Socket.io errors
- Verify that Socket.io is connecting from the same domain
- Clear browser cache and try again

#### Issue: Database connection error
**Solution:**
- Verify `MONGODB_CONNECT` string is correct
- Check MongoDB whitelist includes Render's IP (0.0.0.0/0)
- Test connection locally with same credentials

#### Issue: 503 Service Unavailable
**Solution:**
- Check Render logs for deployment errors
- Verify build command succeeds locally
- Ensure start command is correct: `node backend/index.js`

#### Issue: "vite: not found" during build
**Solution:**
- This happens when devDependencies aren't installed
- Build command MUST include `--include=dev` flag:
  ```
  npm install && npm install --include=dev --prefix frontend && npm run build --prefix frontend
  ```
- This is already configured in package.json and render.yaml

### File Structure Expected

```
chatsphere/
├── backend/
│   ├── index.js
│   ├── DB/
│   ├── Models/
│   ├── middleware/
│   ├── rout/
│   ├── routControlers/
│   ├── Socket/
│   └── utils/
├── frontend/
│   ├── src/
│   ├── package.json
│   ├── vite.config.js
│   └── ...
├── .env
├── .env.example
├── .gitignore
├── .nvmrc
├── render.yaml
├── package.json
└── README.md
```

### Post-Deployment

1. Monitor your app regularly in Render dashboard
2. Check logs for errors
3. Update environment variables as needed
4. Keep your dependencies updated

### Security Best Practices

✅ **DO:**
- Use strong, random JWT_SECRET
- Keep .env file in .gitignore (never commit secrets)
- Use HTTPS (Render provides this by default)
- Enable MongoDB IP whitelist restrictions
- Regularly rotate JWT_SECRET if compromised

❌ **DON'T:**
- Commit .env file to Git
- Use the same JWT_SECRET in development and production
- Expose sensitive information in logs
- Use weak passwords for MongoDB

### Additional Resources

- [Render Documentation](https://render.com/docs)
- [MongoDB Atlas Guide](https://docs.mongodb.com/atlas/)
- [MERN Deployment Best Practices](https://www.mongodb.com/developer/article/mern-stack-deployment/)

### Support

For Render-specific issues:
- Log in to Render Dashboard
- Check the "Incidents" tab
- Review deployment logs
- Contact Render Support

For application issues:
- Check browser console for frontend errors
- Check Render logs for backend errors
- Review MongoDB logs for database issues
