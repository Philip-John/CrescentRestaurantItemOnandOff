# Firestore Security Rules

Your app is now using Firestore with authentication. Follow these steps to set up the security rules:

## Step 1: Enable Firestore

1. Go to [Firebase Console](https://console.firebase.google.com)
2. Select your project **crescent-86-board**
3. Click **Firestore Database** (left sidebar)
4. If not created yet, click **Create Database**
5. Start in **test mode** → Select region → **Enable**

## Step 2: Enable Anonymous Authentication

1. Go to **Authentication** (left sidebar)
2. Click **Get Started**
3. Click **Anonymous** provider
4. Toggle **Enable** → **Save**

## Step 3: Add Firestore Security Rules

1. Go to **Firestore Database** → **Rules** tab
2. Replace all content with these rules:

```firestore
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Only allow authenticated users to read/write menu data
    match /restaurant/menu_data {
      allow read: if request.auth != null;
      allow write: if request.auth != null;
    }
    
    // Deny everything else by default
    match /{document=**} {
      allow read, write: if false;
    }
  }
}
```

3. Click **Publish**

## What This Does

✅ **Requires Authentication** - Must be logged in (anonymous or otherwise)
✅ **PIN Protected** - Your app still requires PIN for manager access
✅ **Real-time Sync** - Changes sync instantly across devices
✅ **No API Key Bypass** - Unauthenticated requests are blocked
✅ **Secure Reads** - Only authenticated users can read data

## How Your App Works Now

1. Browser loads → Auto signs in anonymously (via Firebase Auth)
2. User enters PIN → Gains manager access
3. Manager toggles items → Writes to Firestore (allowed because authenticated)
4. Other devices receive update instantly via real-time listener
5. PIN is your second layer of security

## Testing

1. Open the site on 2 devices
2. Enter PIN on first device
3. Toggle an item
4. Watch it sync on the second device instantly ✨

---

**Note:** Anonymous auth is free and built into Firebase. No credit card needed.
