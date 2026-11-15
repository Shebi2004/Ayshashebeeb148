# Namma Community Chat

A bilingual (Malayalam + English), responsive community chat starter built with React, Vite and Firebase.

## Included
- Email/password registration and sign-in
- Community member list and one-to-one private rooms
- Group creation and group chat
- Image uploads (8 MB limit)
- Voice recording and playback (browser microphone permission required)
- Basic admin dashboard and user-submitted message reports
- Responsive mobile / tablet / desktop layout
- Editable JavaScript/JSX and CSS source

## 1. Requirements
- Node.js 20 or newer
- A Google/Firebase account
- Modern browser; microphone recording requires HTTPS (localhost is allowed for development)

## 2. Create Firebase project
1. Open https://console.firebase.google.com/ and create a project.
2. Add a Web App and copy its Firebase configuration.
3. In `src/firebase.js`, replace all `YOUR_...` values with the configuration.
4. Enable **Authentication → Sign-in method → Email/Password**.
5. Create a **Cloud Firestore** database.
6. Enable **Storage**.
7. In Firestore Rules, paste `firestore.rules` and publish.
8. In Storage Rules, paste `storage.rules` and publish.

## 3. Run locally
```bash
npm install
npm run dev
```
Open the local URL shown by Vite (usually http://localhost:5173).

## 4. Give your account admin access
1. Register your account in the app.
2. In Firebase Console → Firestore Database → `users` collection, open the document whose ID is your Firebase Authentication UID.
3. Change `role` from `member` to `admin`.
4. Reload the app. The Admin panel appears.

Do not let users edit their own `role`. The supplied Firestore rules block role escalation through the client. For a production system, prefer Firebase custom claims set by a trusted Cloud Function/Admin SDK.

## 5. Deploy
Build with:
```bash
npm run build
```
Deploy the `dist` folder using Firebase Hosting, Netlify, or another static host. Configure the host to rewrite unknown routes to `index.html` if you add routing later. Use HTTPS for microphone and secure deployment.

## Important production checklist
This is a starter implementation, not a fully audited production messenger.
- The current group creation flow creates a group with its creator as its only member. Add an invite/member-management screen before using real groups broadly.
- Firestore message reads are currently available to signed-in users. For private group membership enforcement, add membership checks in both queries and Firestore rules before production.
- Add rate limiting / spam prevention using trusted server-side functions.
- Add account deletion, blocking, mute controls, moderator workflows, message retention policy and privacy policy.
- Configure Firebase App Check, budget alerts and backups.
- Validate uploaded file content on a trusted backend; client-side checks are not a security boundary.
- Never put Firebase service-account keys or admin credentials in frontend source.
- Only share images/voice messages you have permission to share. Report abusive content to moderators.

## Project structure
```
src/
  App.jsx       Main UI and chat behavior
  firebase.js   Firebase client configuration
  main.jsx      React entry point
  style.css     Responsive visual design
firestore.rules
storage.rules
```

## Language and branding
Use the language toggle in the header/login screen. Edit the `t` object in `src/App.jsx` to change wording. Adjust colors, spacing and typography in `src/style.css`.
