# Toyota Noah UI updates

Signed user-interface bundles for the Toyota Noah Android dashboard.

The Android updater reads `releases/latest/download/latest.json`, verifies its RSA signature using the public key pinned in the app, and then checks the size, SHA-256 checksum and archive contents before staging a bundle.

Updates download only while the dashboard is open on validated Wi-Fi. They apply on the next app launch, or through Display > UI updates > Restart UI when parked. The app keeps its bundled interface available offline and can restore a previous interface after an incomplete update launch.

## Release contents

- `latest.json`: signed version, compatibility and bundle metadata.
- `ui.zip`: HTML, CSS, JavaScript, fonts and vehicle/map illustration assets.
- Release notes describe the UI changes.

No private signing keys, GPS history, user accounts or media-session data are uploaded to this repository. The update server does not receive the vehicle's GPS coordinates. GitHub receives normal download request metadata such as IP address.

This feed updates the UI only. New Android permissions, native services or native features still require an APK update.

## Publishing future UI changes

From the original local project, build with `node tools/build-ui-update.mjs --version <higher numeric version> --tag ui-<new-tag>` and run `node tools/test-ui-update.mjs`. Publish `dist/ui-update/latest.json` and `dist/ui-update/ui.zip` together in a new GitHub release and mark it latest. Version numbers must increase. Keep the private signing key in the original ignored local signing directory; do not upload it or attach it to a release.

The first feed release matches the UI bundled in the updater APK. It should report that the UI is up to date; later releases can be installed without reinstalling the APK.
