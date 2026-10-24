# Firebase setup — live bookings (free Spark plan)

Use this instead of Supabase. Firebase is free and usually very responsive.

## 1. Create project

1. Open https://console.firebase.google.com  
2. **Add project** → name it (e.g. `jandkcabs`) → continue (Google Analytics optional)  
3. Wait until the project is ready  

## 2. Create Firestore database

1. Left menu → **Build** → **Firestore Database**  
2. **Create database**  
3. Start in **test mode** (for demo; lock rules later)  
4. Choose a region close to you (e.g. `asia-south1` for India)  
5. Enable  

Test mode rules allow open access for 30 days — fine for demo.

Recommended rules (can paste later under Rules tab):

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

*(For production, replace with Auth-based rules.)*

## 3. Register a Web app & copy config

1. Project **Settings** (gear) → **General**  
2. **Your apps** → **Web** (`</>`)  
3. App nickname: `jandkcabs-web` → Register  
4. Copy the `firebaseConfig` object values  

## 4. Paste into index.html

Find this block near the top of the script:

```js
const firebaseConfig = {
  apiKey: "",
  authDomain: "",
  projectId: "",
  storageBucket: "",
  messagingSenderId: "",
  appId: ""
};
```

Fill with your values from Firebase, for example:

```js
const firebaseConfig = {
  apiKey: "AIza...",
  authDomain: "jandkcabs.firebaseapp.com",
  projectId: "jandkcabs",
  storageBucket: "jandkcabs.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc..."
};
```

## 5. Deploy

```bash
git add index.html
git commit -m "Add Firebase config"
git push
```

Vercel redeploys automatically.

## 6. Test

1. Phone/incognito: book a cab → OTP → **Pending**  
2. Laptop: Admin login → Bookings Manager → booking appears live  
3. **Approve + Assign** → updates on all devices  

## Without Firebase

Leave `apiKey` empty. Site still works with **localStorage** on one device.

## Collections used

| Collection | Purpose |
|------------|---------|
| `bookings` | All customer bookings (Pending → Confirmed…) |
| `drivers`  | Optional cloud copy of driver registry |
