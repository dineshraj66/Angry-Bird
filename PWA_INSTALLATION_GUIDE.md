# PWA Installation Guide - Angry Bird

## Overview

Angry Bird is a **Progressive Web App (PWA)** that can be installed as a native app on any device.

---

## Installation by Platform

### 🪟 Windows (Edge/Chrome)

**Method 1: Install Button (Recommended)**
1. Open the app in **Microsoft Edge** or **Chrome**
2. Look for **install icon** in address bar (⬇️ or ➕)
3. Click it
4. Click **"Install"**
5. App opens in its own window (no browser chrome!)

**Method 2: App Menu**
1. Open the app in Edge
2. Click **⋯ (Menu)** → **Apps** → **Install this site as an app**
3. Click **Install**

**Method 3: Start Menu**
1. Right-click app icon in taskbar
2. Click **Pin to Start**
3. App appears in Windows Start menu

**Result:** ✅ App shows as native app in Start Menu & Taskbar, NOT as browser shortcut

---

### 📱 Android (Chrome)

1. Open the app in **Google Chrome**
2. Tap **⋮ (Menu)** → **Install app** or **Add to Home screen**
3. Tap **Install**
4. App appears on home screen with custom icon

---

### 🍎 iPhone/iPad (Safari)

1. Open the app in **Safari**
2. Tap **Share** icon (box with arrow)
3. Scroll down → tap **"Add to Home Screen"**
4. Name the app (or keep default)
5. Tap **Add**
6. App appears on home screen

---

### 🐧 Linux (Chrome/Firefox)

1. Open the app in **Chrome** or **Firefox**
2. Click **⋯ (Menu)** → **Create shortcut** or **Install**
3. App opens in window

---

## Why It's Showing as Shortcut Instead of App

**Common Causes:**

1. **Manifest not loading** → Check DevTools for errors
2. **Service Worker failed** → Check F12 → Application tab
3. **HTTPS required** → Make sure URL starts with `https://`
4. **Edge cache** → Clear data and try again

---

## Fix: Make It Show as Real App on Edge

### Step 1: Clear Edge Cache
1. Press **Ctrl+Shift+Delete**
2. Select **All time**
3. Check:
   - ✅ Cookies and other site data
   - ✅ Cached images and files
4. Click **Clear now**

### Step 2: Close All Edge Windows
- Close Edge completely
- Wait 5 seconds

### Step 3: Reopen App
1. Open the app URL fresh
2. Wait for page to fully load
3. Look for **install icon** (⬇️) in address bar
4. If you see it → Click it!
5. Should say **"Install as app"** not **"Create shortcut"**

### Step 4: Install as App
- Click **Install**
- NOT "Create shortcut"
- This makes it a native app

---

## Verify It's Installed as App

After installation, check:

✅ **App appears in Start Menu** (not just browser)
✅ **Taskbar shows app name** (not "Edge")
✅ **Opening it doesn't show address bar**
✅ **It has its own icon** (Angry Bird, not Chrome)

---

## Troubleshooting

### Problem: Only Seeing "Create Shortcut"

**Solution:**
1. Go back to address bar
2. Type the URL again
3. Wait 2-3 seconds
4. The install button should change to installable app
5. Refresh page: **F5**

### Problem: Install Button Not Appearing

**Checklist:**
- [ ] Using **Edge** or **Chrome** (not other browsers)
- [ ] URL starts with **https://**
- [ ] Tried **Clear cache** (Ctrl+Shift+Delete)
- [ ] Service Worker loaded (F12 → Application → Service Workers)
- [ ] Manifest loads (F12 → Application → Manifest)

### Problem: Still Shows Browser Chrome

**Solution:**
1. Right-click app in taskbar
2. Select **"App settings"** or **"Properties"**
3. Make sure it says **"Launch as standalone window"**
4. Restart the app

---

## What's Happening Inside

When you "Install as app":

✅ Creates app in **Start Menu**
✅ Adds to **Taskbar**
✅ Service Worker **caches files**
✅ Opens in **standalone window** (no address bar)
✅ Works **offline**
✅ Can be pinned to Start

---

## After Installation

### First Time
- May need internet for initial load
- Downloads all files to cache
- Takes 10-30 seconds

### After That
- Works completely **offline**
- Opens in **1-2 seconds**
- Data syncs when online

---

## Uninstall

**Windows:**
1. Right-click app in Start Menu
2. Click **"Uninstall"**
OR
1. Settings → Apps → Apps & features
2. Find **Angry Bird**
3. Click **Uninstall**

**Android:**
- Long press home screen app
- Tap **"Remove"**

**iPhone:**
- Long press app icon
- Tap **"Remove App"** → **"Delete"**

---

## Expected Results

| Device | Appears As | Icon |
|--------|-----------|------|
| **Windows Start Menu** | Native app | 🐦 Angry Bird |
| **Taskbar** | App icon | 🐦 Angry Bird |
| **Android Home** | Home screen icon | 🐦 Angry Bird |
| **iPhone Home** | Home screen icon | 🐦 Angry Bird |

---

## Still Having Issues?

**Check in DevTools (F12):**

1. **Console** → Look for errors
2. **Application** → Service Workers → Should show "Active"
3. **Application** → Manifest → Should load properly
4. **Network** → All files should load

**If you see errors,** screenshot and share them!

---

## Key Points

✅ **HTTPS required** - Must use `https://`
✅ **Service Worker needed** - For offline support
✅ **Manifest required** - Tells browser app details
✅ **Cache first** - Clear old data before installing
✅ **Use Edge/Chrome** - Best PWA support

Once installed, you have a **real native app** that:
- Runs offline
- Syncs online
- Opens instantly
- Uses your home screen space
- Works like any other app

Enjoy! 🚀
