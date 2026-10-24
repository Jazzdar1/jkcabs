# jandkcabs — Complete Jammu & Kashmir Travel Platform

Cabs • packages • hotels • houseboats • sightseeing • customer / driver / admin portals.

## Deploy (GitHub + Vercel)

1. Push this repo to GitHub  
2. Import in [Vercel](https://vercel.com) → Framework: **Other** → Deploy  

## Live multi-device bookings (Firebase — free)

Supabase is not used. Sync runs on **Firebase Firestore** (free Spark plan).

Full steps: **[FIREBASE_SETUP.md](./FIREBASE_SETUP.md)**

Quick version:
1. Create project at https://console.firebase.google.com  
2. Enable **Firestore** (test mode)  
3. Register a **Web app** → copy `firebaseConfig`  
4. Paste into `index.html` (`apiKey`, `projectId`, etc.)  
5. Commit & push → Vercel redeploys  

Then customers and admin on **different devices** share bookings in real time.

## Admin login

- User: `admin` or `admin@jandkcabs.in`  
- Password: `jkcabs@2010`

## Data modes

| Config | Behavior |
|--------|----------|
| Firebase keys filled | Live sync across all devices |
| `apiKey` empty | localStorage only (same browser) |
