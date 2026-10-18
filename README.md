# Study Log

Study, entertainment and sleep, drawn as one 24-hour day. A personal tracker with a study timer, focus ratings, an entertainment timer with a daily limit, a sleep log, a weekly review and pattern insights.

**Live:** https://pmkyaw412-lab.github.io/study-log/

## How it stores data

Sign in with Google. Everything is saved to Cloud Firestore in the `study-log-eric` Firebase project, under `users/{uid}`:

- `sessions/{id}` — one document per study, entertainment or sleep session
- `meta/active`, `meta/fun`, `meta/sleeping` — timers that are running right now
- `meta/config` — subjects, targets and settings

Firestore's offline cache keeps the app working without a connection and syncs every device live. `firestore.rules` lets each signed-in person read and write only their own documents, and validates every session.

The Firebase web config in `index.html` is public by design; access is controlled by sign-in and the security rules, not by hiding the key.

## Moving data in

Settings → Backup and restore → paste a CSV backup from the old Study Log. Rows already present are skipped.

## Files

- `index.html` — the whole app
- `firestore.rules` — Firestore security rules, deployed separately with the Firebase CLI
- `manifest.webmanifest`, `icon-*.png` — lets you add it to your phone's home screen
