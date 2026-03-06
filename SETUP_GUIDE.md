# Angry Bird - Emotion Tracker PWA
## Setup & Deployment Guide

---

## 📋 Project Structure

```
angry-bird-pwa/
├── index.html              (Main entry point - redirects to app)
├── angry-bird-app.html     (Main application file)
├── manifest.json           (PWA manifest for installation)
├── sw.js                   (Service Worker for offline support)
└── README.md               (This file)
```

---

## 🚀 Quick Start (Local Testing)

### 1. Download Files
Download all files and place them in a folder:
```bash
mkdir angry-bird-pwa
cd angry-bird-pwa
# Place all 4 files here
```

### 2. Run Local Server
You need a local server to test (required for Service Worker):

**Using Python 3:**
```bash
python -m http.server 8000
```

**Using Python 2:**
```bash
python -m SimpleHTTPServer 8000
```

**Using Node.js (http-server):**
```bash
npx http-server -p 8000
```

### 3. Access the App
Open: `http://localhost:8000`

---

## 🔥 Firebase Setup

### Option A: Using the Pre-configured Demo Firebase (No Setup Required)
The app includes a demo Firebase configuration that works with localStorage fallback. You can use it as-is and entries will be stored locally.

### Option B: Create Your Own Firebase Project

1. **Go to Firebase Console**: https://console.firebase.google.com/
2. **Create New Project**:
   - Click "Create Project"
   - Name: "angry-bird-tracker"
   - Continue through the setup (enable Google Analytics if desired)
   - Click "Create Project"

3. **Enable Realtime Database**:
   - In the left sidebar, click "Realtime Database"
   - Click "Create Database"
   - Start in "Test Mode" (we'll secure it later)
   - Choose region closest to you
   - Click "Enable"

4. **Get Your Config**:
   - Go to "Project Settings" (gear icon)
   - Under "Your apps", find Web app
   - Copy the Firebase config object

5. **Update the App**:
   - Open `angry-bird-app.html`
   - Find this section (around line 278):
   ```javascript
   const firebaseConfig = {
       apiKey: "YOUR_API_KEY",
       authDomain: "YOUR_PROJECT.firebaseapp.com",
       databaseURL: "https://YOUR_PROJECT-default-rtdb.firebaseio.com",
       projectId: "YOUR_PROJECT",
       storageBucket: "YOUR_PROJECT.appspot.com",
       messagingSenderId: "YOUR_SENDER_ID",
       appId: "YOUR_APP_ID"
   };
   ```
   - Replace with your actual config

6. **Security Rules** (Optional but Recommended):
   - Go to "Realtime Database" → "Rules"
   - Replace with:
   ```json
   {
     "rules": {
       "users": {
         "$uid": {
           ".read": "true",
           ".write": "true"
         }
       }
     }
   }
   ```

---

## 📦 Deploy to GitHub Pages

### Step 1: Create GitHub Repository

1. Go to https://github.com/new
2. Repository name: `angry-bird-pwa` (or any name)
3. Add description: "Angry Bird - Emotion Tracking PWA"
4. Choose "Public" (required for GitHub Pages free tier)
5. Click "Create repository"

### Step 2: Push Files to GitHub

Using Git (if you have it installed):

```bash
cd angry-bird-pwa

# Initialize git
git init

# Add remote
git remote add origin https://github.com/YOUR_USERNAME/angry-bird-pwa.git

# Add all files
git add .

# Commit
git commit -m "Initial commit: Angry Bird PWA"

# Push to main branch
git branch -M main
git push -u origin main
```

**If you don't have Git installed:**
1. Go to your GitHub repository
2. Click "Upload files"
3. Drag and drop all 4 files
4. Click "Commit changes"

### Step 3: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click "Settings" → "Pages"
3. Under "Source", select "main" branch
4. Click "Save"
5. Your site will be live at: `https://YOUR_USERNAME.github.io/angry-bird-pwa/`

**Note:** It may take a few minutes to deploy. Refresh to check status.

### Step 4: Custom Domain (Optional)

If you own a domain:
1. In "Pages" settings, add your custom domain
2. Update your domain's DNS records pointing to GitHub Pages IP
3. GitHub will handle SSL automatically

---

## 📱 PWA Installation

### Desktop (Chrome/Edge)
1. Open the app in Chrome or Edge
2. Click the install icon (⬇️) in the address bar
3. Click "Install"
4. App opens in standalone window

### Mobile (Android)
1. Open in Chrome
2. Tap menu (⋮) → "Install app" or "Add to Home screen"
3. Confirm installation
4. App appears on home screen

### Mobile (iOS/Safari)
1. Open in Safari
2. Tap Share → "Add to Home Screen"
3. Name the app → "Add"
4. App appears on home screen

---

## 💾 Data Storage

### Local Storage
- Entries stored in browser's localStorage
- Works offline immediately
- Limited to ~5-10MB per domain

### Firebase Sync
- If Firebase connection available, entries also sync to database
- Syncs across devices
- Cloud backup

### Offline First
- App works fully offline
- Entries stored locally first
- Firebase syncs when online
- No data loss

---

## 🛠️ Customization

### Change Colors
In `angry-bird-app.html`, find the CSS variables section (~line 47):
```css
:root {
    --primary: #d32f2f;        /* Red - Main brand color */
    --primary-dark: #b71c1c;
    --primary-light: #ff5252;
    --secondary: #ffd54f;      /* Yellow - Accent */
    /* ... more colors */
}
```

### Change Emotions
In `angry-bird-app.html`, find the emotion buttons (~line 367):
```html
<button class="emotion-btn" data-emotion="Angry" title="Angry">😠<span class="emotion-label">Angry</span></button>
<!-- Add more buttons -->
```

### Change App Name
1. In `manifest.json` - change `"name"` and `"short_name"`
2. In `angry-bird-app.html` - change header text
3. In `index.html` - change title

---

## 🐛 Troubleshooting

### Service Worker Not Working
- Clear browser cache (DevTools → Application → Clear storage)
- Make sure you're on HTTPS or localhost
- Check browser console for errors

### Firebase Not Syncing
- Check Firebase config is correct
- Verify database rules allow writes
- Check browser console for connection errors
- App still works offline with localStorage

### PWA Won't Install
- Make sure manifest.json is correct
- Check HTTPS or localhost
- Try different browser
- Clear cache and reload

### Emotions Not Saving
- Check localStorage isn't full
- Verify all form fields are filled
- Check browser console for errors

### GitHub Pages Not Loading
- Wait 5-10 minutes after pushing
- Check branch is set to "main" in Pages settings
- Verify files are in repository root
- Check repository name in URL

---

## 📊 Features

✅ Track emotions (Angry, Frustrated, Stressed, Anxious)
✅ Log location and timestamp
✅ Record root cause
✅ Document solutions/actions
✅ View emotion history with full details
✅ Dashboard with insights:
  - Total entries & monthly count
  - Most common emotion
  - Most common location
  - Most common trigger
  - Last entry date
✅ Delete entries
✅ Offline-first PWA
✅ Firebase cloud sync
✅ Install on home screen
✅ localStorage backup
✅ Toast notifications
✅ Beautiful, responsive UI

---

## 📈 Next Steps

1. **Deploy to GitHub Pages** (follow steps above)
2. **Test PWA installation** on mobile
3. **Customize colors** to match your brand
4. **Add more emotions** if needed
5. **Set up Firebase** for cloud sync
6. **Share with others** using the GitHub Pages URL

---

## 🔐 Privacy & Security

- Data stored locally in your browser first
- Firebase stores data in your Google account
- No data sent to third parties
- You own all your data
- Delete entries anytime

---

## 📝 Notes

- The app uses a unique user ID generated on first use
- All data stored with your user ID for multi-device sync
- Service Worker caches app for offline use
- Firebase uses compat SDK for wider browser support

---

## 💡 Tips

- Use location field for context (e.g., "Work Meeting", "Home")
- Root cause helps identify triggers
- Solution field tracks what worked for you
- Review history monthly for patterns
- Dashboard insights help you see trends

---

**Happy tracking! 🐦**

Questions? Check the browser console (F12) for any errors.
