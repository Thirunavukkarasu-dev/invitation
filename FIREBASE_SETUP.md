# Firebase Setup Guide for Wedding Blessings

This guide will help you set up Firebase so that blessings can be seen from all devices, not just the local browser.

## Step 1: Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Add project" or "Create a project"
3. Enter project name: `wedding-blessings` (or any name you prefer)
4. Click "Continue"
5. Disable Google Analytics (optional, you can skip it)
6. Click "Create project"
7. Wait for project creation, then click "Continue"

## Step 2: Enable Firestore Database

1. In your Firebase project, click on "Firestore Database" in the left menu
2. Click "Create database"
3. Select "Start in test mode" (for now, this is fine for a wedding invitation)
4. Choose a location (select the closest to your region)
5. Click "Enable"

## Step 3: Get Your Firebase Configuration

1. In Firebase Console, click the gear icon ⚙️ next to "Project Overview"
2. Select "Project settings"
3. Scroll down to "Your apps" section
4. Click the web icon `</>` to add a web app
5. Register app with a nickname (e.g., "Wedding Invitation")
6. Click "Register app"
7. Copy the `firebaseConfig` object that looks like this:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef"
};
```

## Step 4: Update Your HTML File

1. Open `index.html`
2. Find the section that says:
```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT_ID.appspot.com",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

3. Replace it with your actual Firebase config values from Step 3

## Step 5: Set Up Firestore Security Rules (Important!)

1. In Firebase Console, go to "Firestore Database"
2. Click on "Rules" tab
3. Replace the rules with this (allows anyone to read/write - fine for a wedding invitation):

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /blessings/{document=**} {
      allow read, write: if true;
    }
  }
}
```

4. Click "Publish"

## Step 6: Test It!

1. Open your wedding invitation in a browser
2. Leave a test blessing
3. Open the same page on another device/browser
4. You should see the blessing from the first device!

## Important Notes:

- **Free Tier**: Firebase has a generous free tier that should be more than enough for a wedding invitation
- **Security**: The rules above allow anyone to read/write. For a wedding invitation, this is usually fine, but you can make it more secure later if needed
- **Fallback**: If Firebase isn't configured, the system will automatically fall back to localStorage (local storage)

## Troubleshooting:

- If blessings don't appear: Check browser console (F12) for errors
- Make sure Firestore is enabled (not just Realtime Database)
- Verify your Firebase config is correct
- Check that Firestore rules are published

## Alternative: Simple Backend Solution

If you prefer not to use Firebase, you could also:
- Use a simple backend API (Node.js, Python, etc.)
- Use Google Sheets API
- Use a form service like Formspree

But Firebase is the easiest and most reliable for this use case!

