# Angry Bird Firebase Troubleshooting

## 🔴 "Firebase Still Not Collected" - Diagnostic Guide

Follow these steps to identify the issue:

---

## Step 1: Check Console Logs

1. Open the app in browser
2. Press **F12** to open DevTools
3. Go to **Console** tab
4. Create an entry and watch the console

### What You Should See:

**Good Signs:**
```
📱 App loaded, initializing...
🔄 Checking Firebase SDK...
✅ Firebase SDK detected after 100 ms
✅ Firebase initialized successfully
✅ Firebase listeners setup complete
🟢 Firebase database connected
💾 Saving entry: {id, emotion, date, ...}
✅ Saved to localStorage
🔥 Attempting Firebase write...
📍 Path: users/shared-user/entries/123456
✅ Entry saved to Firebase: 123456
```

**Bad Signs (indicates problem):**
```
❌ Firebase SDK failed to load after 5 seconds
❌ Firebase initialization error
❌ Firebase write error
```

---

## Step 2: Check Your Specific Error

### Error: "Firebase SDK failed to load"

**Cause:** Firebase CDN is blocked or not accessible

**Solutions:**
1. Check internet connection
2. Check if you're behind a corporate firewall (may block CDN)
3. Try refreshing the page
4. Try a different browser
5. Check if `gstatic.com` domain is accessible

**Test:**
```javascript
// Copy-paste in console:
fetch('https://www.gstatic.com/firebasejs/9.22.1/firebase-app-compat.min.js')
  .then(r => console.log('✅ CDN accessible:', r.ok))
  .catch(e => console.error('❌ CDN blocked:', e.message))
```

---

### Error: "Firebase write error: Permission denied"

**Cause:** Your Firebase security rules are wrong

**Solution:**
1. Go to: https://console.firebase.google.com/
2. Select project: **angry-bird-2776f**
3. Click **Realtime Database** → **Rules**
4. Replace with these rules:

```json
{
  "rules": {
    "users": {
      "$uid": {
        ".read": true,
        ".write": true,
        "entries": {
          "$entryId": {
            ".validate": "newData.hasChildren(['id', 'emotion', 'date', 'location', 'rootCause', 'solution', 'timestamp'])"
          }
        }
      }
    }
  }
}
```

5. Click **Publish** button
6. Reload the app and try again

---

### Error: "Entry saved locally but not to Firebase"

**Possible Causes:**

1. **Firebase rules not updated** - See above

2. **Network issue** - Try:
   - Check internet connection
   - Try refreshing page
   - Wait a few seconds before creating entry

3. **Browser privacy mode** - Try:
   - Use normal browsing mode (not incognito)
   - Clear browser cache
   - Hard refresh (Ctrl+Shift+R)

4. **Cross-site cookies blocked** - Try:
   - Check browser privacy settings
   - Whitelist Firebase domain
   - Try different browser

---

## Step 3: Check Firebase Console

1. Go to: https://console.firebase.google.com/
2. Select project: **angry-bird-2776f**
3. Click **Realtime Database**
4. Click **Data** tab
5. Look for: `users` → `shared-user` → `entries`
6. You should see your entries here

If no entries appear:
- Firebase didn't receive the write
- Check console errors (Step 1)
- Check security rules (Step 2)

---

## Step 4: Test with Debug Panel

1. Triple-tap the "🐦 Angry Bird" header
2. A debug panel appears at bottom showing:
   - User ID: `shared-user`
   - Firebase: `✅ Connected` or `❌ Offline`
   - Local Entries: number of entries in localStorage
   - Cloud Entries: number of entries loaded from Firebase
   - Status: `DB Ready` or `No DB`

This shows you the real-time status.

---

## Step 5: Nuclear Option - Reset Everything

If all else fails:

1. **Clear browser storage:**
   - Press F12 → Application → Clear storage → Clear site data
   - Refresh page

2. **Check Firebase project:**
   - Make sure database exists
   - Check Rules are published
   - Check URL is correct in app config

3. **Try localhost test:**
   - If testing on phone, try desktop first
   - `http://localhost:8000`
   - Create entry
   - Check console logs

4. **Check network:**
   - Open DevTools → Network tab
   - Look for Firebase API calls
   - Check if they succeed or fail

---

## What the Console Should Show

### On First Load:
```
📱 App loaded, initializing...
🔄 Checking Firebase SDK...
✅ Firebase SDK detected after [time] ms
✅ Firebase initialized successfully
✅ Firebase listeners setup complete
🟢 Firebase database connected
📥 loadEntries called
📦 Local entries: 0
🔥 Loading from Firebase...
✅ Firebase entries loaded: 0
```

### When Creating Entry:
```
💾 Saving entry: {object}
isOnline: true db: true
✅ Saved to localStorage
🔥 Attempting Firebase write...
📍 Path: users/shared-user/entries/1234567890
✅ Entry saved to Firebase: 1234567890
📥 loadEntries called
✅ Firebase entries loaded: 1
```

---

## Common Issues & Fixes

| Issue | Cause | Fix |
|-------|-------|-----|
| "Firebase SDK failed to load" | CDN blocked | Check network, try different network |
| "Permission denied" | Rules not updated | Update and publish security rules |
| Entry saves but not synced | Rules incorrect | Verify rules are correct and published |
| No entries on mobile | Different URLs | Both must use same URL |
| Data appears then disappears | Cache issues | Clear site data, hard refresh |
| Offline but not syncing | Network issue | Check connection |

---

## Quick Checklist

- [ ] Firebase SDK loaded (check console)
- [ ] Firebase initialized successfully
- [ ] Database connected (green indicator)
- [ ] Security rules are correct
- [ ] Rules are **Published**
- [ ] Using same URL on all devices
- [ ] Internet connection is active
- [ ] No console errors
- [ ] Data appears in Firebase console

---

## Get Help

If still not working, share:
1. **Screenshot of console** (F12 Console tab)
2. **Screenshot of debug panel** (triple-tap header)
3. **Screenshot of Firebase console** (Realtime Database → Data)
4. **Error messages** (if any)
5. **What device/browser** you're using

Then we can diagnose the exact issue!
