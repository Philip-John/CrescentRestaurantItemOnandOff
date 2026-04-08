# 86 Board - Deployment Guide

## What's been set up

✅ Firebase Realtime Database integration  
✅ Real-time sync across all devices  
✅ GitHub Pages deployment workflow  
✅ Automatic deployments on push  

## Next Steps

### 1. Initialize Git Repository

```bash
cd d:\CrescentItemONOFF
git init
git add .
git commit -m "Initial commit: 86 Board with Firebase integration"
```

### 2. Create GitHub Repository

1. Go to [github.com/new](https://github.com/new)
2. Name it `crescent-86-board` (or whatever you prefer)
3. **Do NOT** initialize with README
4. Click "Create repository"

### 3. Push to GitHub

After creating the repo, GitHub will show commands. Run these in PowerShell:

```bash
git remote add origin https://github.com/YOUR-USERNAME/crescent-86-board.git
git branch -M main
git push -u origin main
```

Replace `YOUR-USERNAME` with your actual GitHub username.

### 4. Enable GitHub Pages

1. Go to your GitHub repo
2. Click **Settings** → **Pages** (left sidebar)
3. Under "Source", select **Deploy from a branch**
4. Branch: **main**, folder: **/ (root)**
5. Click **Save**

Your site will be live at: `https://YOUR-USERNAME.github.io/crescent-86-board`

### 5. Firebase Security (Important!)

Your current Firebase database is in **test mode** (anyone can read/write). For a real restaurant:

1. Go to [Firebase Console](https://console.firebase.google.com)
2. Select your project → **Realtime Database** → **Rules**
3. Replace the rules with:

```json
{
  "rules": {
    "menu": {
      ".read": true,
      ".write": "auth != null"
    }
  }
}
```

Then set up authentication in your app. For now, test mode is fine.

## How It Works

- **Real-time sync**: Changes instantly appear on all devices
- **Offline fallback**: Uses localStorage if Firebase is down
- **Auto-deploy**: Push to main branch = automatic deployment
- **Manager PIN**: Still required to make changes (1234)

## Testing Live Sync

1. Open the site on two different devices/browsers
2. Mark an item as 86'd on one device
3. Watch it update instantly on the other device ✨

## Troubleshooting

**"Firebase not working"**
- Check your Firebase config in the code
- Ensure Firebase Realtime Database is enabled in Firebase console
- Check browser console for errors (F12)

**"GitHub Pages not deploying"**
- Go to Settings → Pages → check deployment status
- Look at Actions tab to see if workflow succeeded

**"Changes not syncing"**
- Check internet connection
- Refresh the page
- Check browser console for errors

---

Questions? Let me know!
