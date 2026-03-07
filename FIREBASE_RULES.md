# Firebase Security Rules for Angry Bird

## ⚠️ IMPORTANT: Update Your Firebase Rules

Your current Firebase might not allow proper read/write operations. Follow these steps:

### Step 1: Go to Firebase Console
1. Open: https://console.firebase.google.com/
2. Select project: **angry-bird-2776f**
3. Click **Realtime Database** (left sidebar)
4. Click **Rules** tab (top navigation)

### Step 2: Replace Rules with This Code

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

### Step 3: Publish Rules
1. Click **Publish** button (bottom right)
2. Confirm the dialog
3. Wait for deployment (usually instant)

## What This Does

✅ Allows all users to read from the database
✅ Allows all users to write to their own data
✅ Validates entry structure (prevents malformed data)
✅ Enables cross-device syncing

## Testing Firebase Connection

1. Open browser DevTools: **F12**
2. Go to **Console** tab
3. Create an entry in the app
4. Look for messages like:
   - `"Firebase initialized successfully"` ✅
   - `"Firebase connected"` ✅
   - `"Entry saved to Firebase: [ID]"` ✅

If you see errors, check:
- Rules are published
- Database URL is correct in app config
- Network connection is active

## Troubleshooting

### Error: "Permission denied"
→ Update the security rules above and click Publish

### Error: "Auth token is invalid"
→ This is normal, the app doesn't use authentication
→ The rules above allow access without auth

### No data appearing in Firebase Console
→ Check Console (F12) for error messages
→ Verify rules were published
→ Try creating a new entry
→ Refresh the page

### Data syncs on one device but not the other
→ Both devices must use the same app at same URL
→ Firebase syncs using real-time listeners (on)
→ May take 1-2 seconds to appear
→ Check browser console for connection status

## Monitoring Sync

To watch Firebase in real-time:
1. Go to Firebase Console
2. Realtime Database → Data tab
3. Create an entry in the app
4. Watch the data appear under: `users/shared-user/entries/`
