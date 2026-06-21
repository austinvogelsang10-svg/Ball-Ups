# Bounce — iOS via TestFlight (no Mac needed)

A Capacitor wrapper around the Bounce web game, built and shipped to
TestFlight by Codemagic. You can do all of this from a phone.

## What you need first
- Apple Developer Program membership ($99/yr). Enroll in the Apple
  Developer app on your iPhone.
- A GitHub account (free).
- A Codemagic account (free tier ~500 macOS minutes/month).

## One-time setup (~30 min, all from the phone)
1. Create a GitHub repo and upload these files, keeping the www/ folder.
2. In App Store Connect (appstoreconnect.apple.com): Apps > + > New App.
   Pick a bundle ID like com.YOURNAME.bounce. Note the bundle ID.
3. In App Store Connect: Users and Access > Integrations/Keys >
   App Store Connect API > generate a key (App Manager role). Download
   the .p8 ONCE, and copy the Issuer ID and Key ID.
4. In Codemagic: Teams > Code signing identities > App Store Connect API
   keys > add the .p8 + Issuer ID + Key ID. Name it BounceASCKey.
5. Edit the 3 CHANGE-ME spots in codemagic.yaml + the appId in
   capacitor.config.json so the bundle id matches step 2 and the key name
   matches step 4.
6. In Codemagic: add the app from your GitHub repo, then Start build.

It builds the native project in the cloud, signs it, and pushes to
TestFlight. After Apple finishes processing (a few min), the build shows
up in TestFlight and your testers get it.

## Notes
- First upload: if Codemagic's automated first upload is rejected because
  the app record has no build yet, just re-run the build — the API upload
  usually succeeds on its own. (Manual upload needs a Mac, so rely on this.)
- To ship a fix later: change something, push to GitHub, build again. The
  build number auto-increments from the timestamp.
- Three.js is bundled locally (www/three.min.js), so the app works offline.
