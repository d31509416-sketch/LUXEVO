# LUXEVO — public browsing + login required for customization

This is your **existing LUXEVO website updated**, not a separate template. It includes all five original product images, the original responsive black-and-gold design, and a functional visual customizer. It is intended for GitHub Pages, not a website builder.

## Customer experience

- **Guests:** Can view the homepage, scroll through all five devices, search, view product details, and add items to an inquiry. No login required.
- **Customize button:** Clicking Customize on any of the five products prompts guests to **Log in** or **Create account**. They return automatically to that product's customization window after successful sign-in.
- **Signed-in customers:** Choose an electric-violet/gold/sapphire accent **preview** and an optional personalization label, then save. The **Log out** button is always available in the site header.
- **Logout:** Saved designs are hidden as soon as the customer logs out. Visitors can keep browsing.
- **Password reset:** Available from the login screen. **There is no demo account.**

## REQUIRED: set up Firebase Authentication

1. Visit https://console.firebase.google.com/ and create a Firebase project.
2. Register a **Web app** under Project settings and copy the Firebase web configuration.
3. Firebase Console → Authentication → Sign-in method → enable **Email/Password**.
4. Edit **firebase-config.js** and replace its placeholders with your own Web app values (usually `apiKey`, `authDomain`, `projectId`, `appId`). Never add service-account keys or private secrets.
5. Authentication → Settings → Authorized domains: add your site domain if required (e.g., `YOURNAME.github.io`). Do not add the `/repo/` path. GitHub Pages uses HTTPS.
6. Upload all of this package's **contents**, including the `assets` folder, to the root of your GitHub repo. GitHub repo → Settings → Pages → Deploy from a branch → `main` and `/(root)`.
7. Open the published GitHub Pages URL. Browse signed out; click Customize; create an account; save a design; log out; test sign-in again.

> The `firebase-config.js` file identifies your Firebase app but is not an admin secret. Restrict project resources with Firebase Security Rules if you introduce databases.

## Important scope and security limits

- **Visual customization demo:** The three accent choices change the **on-screen preview glow**, not the hardware color. The personalization label is on-screen only. These are NOT verified production options.
- **Where customizations are saved:** Browser `localStorage` under a key scoped to the Firebase user's UID. This means designs persist on **that browser/device only**, and can be cleared by the user. They do **not sync across devices** and are not stored in Firebase. Do not put sensitive customer information in the label.
- The authentication gate prevents a guest from using the site's customization UI. **It is not server-side authorization** for the public GitHub Pages source. If you later need permanent customer designs across devices, add Firestore with rules requiring `request.auth.uid == userId` for the appropriate document path.
- This is a **concept website**: there is no real checkout, payment, order processing, or confirmed manufacturing customization.
- Authentication requires internet access and an initialized Firebase project; double-clicking `index.html` with a `file://` URL usually won't run JavaScript modules correctly. View via GitHub Pages or a local HTTP server.

Official sources:
- https://firebase.google.com/docs/auth/web/start
- https://firebase.google.com/docs/auth/web/password-auth
- https://firebase.google.com/docs/firestore/security/get-started
- https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages
