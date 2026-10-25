# PCG Walkthroughs v0.1.1

Tap your path on a floor plan while the Insta360 records, then click the line to jump the 360 video to that spot. Share a link with owners and franchise reps; viewers don't need a login.

## Setup, all in the browser (no installs)

### 1. Firebase (console.firebase.google.com)
1. Create a project (or reuse your PCG one). Switch it to the **Blaze** plan (needed for Storage; free allowance still applies).
2. **Authentication > Get started > Email/Password** > enable. Then **Users > Add user** for yourself.
3. **Firestore Database > Create database.** Open the **Rules** tab, paste the contents of `firestore.rules`, Publish.
4. **Storage > Get started.** Open the **Rules** tab, paste the contents of `storage.rules`, Publish.
5. **Project settings (gear) > Your apps > Web (</>)** > register an app > copy the `firebaseConfig` values.

### 2. GitHub (github.com)
1. **New repository** > name it `pcg-walkthroughs` > Public > Create.
2. **Add file > Upload files** > drag in everything from this folder > Commit.
3. Click `config.js` > pencil icon > paste your Firebase values > Commit.
4. **Settings > Pages** > Source: *Deploy from a branch* > Branch: `main`, folder `/ (root)` > Save. In a minute your site is at `https://YOUR-USERNAME.github.io/pcg-walkthroughs/`.

### 3. Connect the two
1. Firebase **Authentication > Settings > Authorized domains > Add domain** > `YOUR-USERNAME.github.io`.
2. Let the 360 player read videos from Storage: go to **console.cloud.google.com**, select the same project, click the **Cloud Shell** icon (top right, `>_`). Click the ⋮ menu > **Upload** > pick `cors.json`. Then run:
   `gsutil cors set cors.json gs://YOUR-BUCKET-NAME`
   (bucket name is the `storageBucket` value from config.js). Without this, shared videos won't play.

The Firebase web keys in config.js are meant to be public; the rules files are what protect your data.

## Field use
1. Open the site on your phone > **New walkthrough** > name, project, floor plan (image or PDF).
2. Press **record on the camera**, then tap **Start** right away.
3. Tap where you're standing: start spot first, then every doorway, corner and room. If you stop somewhere, tap that spot again before moving on.
4. Stop the camera, tap **Stop**, then **Done**.
5. Export the clip from Insta360 Studio as a **360° MP4** (H.264, 4K, lower bitrate). Open the walkthrough, pick the video, use **Match start point** if the dot runs ahead or behind.
6. **Sign in** > **Upload & create share link** > copy and send.

Walkthroughs stay on the phone that captured them until uploaded.

## Optional: Firebase Hosting instead of GitHub Pages
The `public/` folder and `firebase.json` are kept for that route (`firebase deploy`).
