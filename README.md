# MTCA Wellness Weight Challenge

## Firebase setup order

1. Open the existing Firebase project `mtca-wellness`.
2. **Authentication → Sign-in method → Google → Enable** and select a support email.
3. **Authentication → Settings → Authorized domains** and add:
   - your GitHub Pages host, for example `maxrayawa51.github.io`
   - any custom domain used for the app
   - `localhost` for local testing only
4. **Realtime Database → Rules**: replace the current rules with `database.rules.json`, then publish.
5. Confirm the master administrator email in both:
   - `firebase-config.js`
   - `database.rules.json`
6. Deploy the GitHub files. Do not open `index.html` using `file://`; use GitHub Pages or a local web server.
7. The master administrator signs in and registers first. Other staff then sign in and register. The master administrator can grant admin access from the Administration screen.

## GitHub Pages deployment

1. Create a repository, for example `mtca-wellness`.
2. Upload `index.html` and `firebase-config.js` to the repository root.
3. Upload `database.rules.json` for version control. It is not loaded by the website.
4. Open **Settings → Pages**.
5. Select **Deploy from a branch**, branch `main`, folder `/root`.
6. Add the generated GitHub Pages domain to Firebase Authorized domains.

## Security design

- `publicProfiles`: names and divisions visible to signed-in users.
- `privateProfiles`: baseline weight, height and email visible only to the owner and administrators.
- `weighins`: stored under each user UID and visible only to the owner and administrators.
- `leaderboard`: displays percentage change only, not exact weight.
- `admins`: managed only by the master administrator.

The Firebase web API key is an identifier, not a password. The security boundary is Firebase Authentication plus Realtime Database Rules.
