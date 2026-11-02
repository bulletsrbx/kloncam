# KlonCam releases

KlonCam is a static web app deployed from `main` at https://bulletsrbx.github.io/kloncam/.

For every user-facing update:
- Increase both `APP_RELEASE.version` (semantic version) and `APP_RELEASE.build` (monotonically increasing integer) in `index.html`.
- Keep `version.json` identical to the embedded `APP_RELEASE` object and add concise German release notes describing the actual changes. The popup identifies the code actually loaded, not merely the newest manifest.
- Keep the static version labels in the HTML consistent, so the loaded version remains visible even if startup fails.
- Verify first-load release notes, dismissal persistence, newer-version detection and refresh, and that update checks cannot interrupt recording or export.
- Preserve the current origin, manifest identity and IndexedDB database. Never clear user recordings to update the app. Before camera start, the in-memory timeline is empty even when IndexedDB contains a project; do not save that empty state before an update reload.
- Distinguish the camera frame rate from the output frame rate. A 60 fps file generated from 30 fps capture repeats images; do not claim native 60 fps capture in that case.
