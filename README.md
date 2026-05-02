# Content Strategy — Updates

Auto-update feed for [Content Strategy](https://kamstudios.com), a content planning + AI-assisted social media manager in the Aligned product suite.

The application source lives in a private repository. This public repository hosts only the [Sparkle](https://sparkle-project.org) update feed (`appcast.xml`) and the released `.zip` artifacts (as GitHub Releases).

## What's here

- **`appcast.xml`** — the feed Sparkle reads on the user's Mac on each update check. Updated each release.
- **Releases tab** — released `.zip` artifacts (one per version), referenced by `appcast.xml`'s `<enclosure>` URLs.

## Release flow (for the maintainer)

1. Archive a notarized `.app` build of Content Strategy
2. Zip it → run Sparkle's `sign_update` against the zip to get an EdDSA signature
3. Create a new GitHub Release here; upload the zip as the release asset
4. Update `appcast.xml` with a new `<item>` (title, version, signature, asset URL, length)
5. Commit + push `appcast.xml`
6. Sparkle on user Macs picks up the change on the next scheduled check

## Privacy / scope

This repository is public so the appcast feed and release artifacts are reachable by users' Sparkle update checks. It contains only:

- One XML feed file
- Published release `.zip` artifacts

It does NOT contain the application source, planning artifacts, design files, or any internal materials.
