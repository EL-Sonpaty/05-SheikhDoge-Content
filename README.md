# Sheikh Doge — content and releases

This repository exists to be **public**. The application's own source stays private; this
holds only the two things every installed copy needs to be able to reach.

| File | What it is |
|---|---|
| `latest.json` | The update manifest. Sheikh Doge reads this to learn whether a newer release exists. |
| `content.md` | The bundled azkar — the notification pool and every browsable series. |

## Why it is separate

Free content delivery serves public repositories only, and an app that checks for updates has
to reach something without a token. Splitting it this way means the application's code can stay
private while the files it must fetch are open — and the azkar are the Qur'an and the Sunnah,
which were never anybody's private property to begin with.

It has a second benefit worth the split on its own: corrections arrive as pull requests. A
reviewer who finds a mistake in a تخريج can propose the fix here, and once it is merged every
installation picks it up on its next sync. No installer, no release.

## Publishing a release

Do not edit `latest.json` by hand. It carries a SHA-256 that the app checks before it will run
anything it downloaded, so a hash typed in by a person is a broken update for everybody —
and it fails at the last step, after the download, which is the most confusing place for it
to fail.

From the application repository:

```powershell
./tools/release.ps1 -Version 1.0.1 -Notes "What changed."
```

That builds the installer, hashes it, and rewrites `latest.json` here. Then:

1. Commit and push this repository.
2. Create a GitHub release tagged `v1.0.1` and attach `SheikhDoge-Setup.exe` to it.

The order matters. Publish the release **before** pushing the manifest, or every copy of the
app will spend the gap trying to download a file that does not exist yet.

## What must never go in here

This repository is public. Nothing that is not meant to be read by anyone belongs in it — no
tokens, no keys, no logs, no user data, and no part of the application's source.

## Licence

The azkar are from the Qur'an and the Sunnah and are not subject to copyright. أذكار الصباح
والمساء follow حصن المسلم and carry their own تخريج. Everything else here is MIT, the same as
the application.
