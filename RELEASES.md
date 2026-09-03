# Android updater and releases

The permanent manifest URL is `https://raw.githubusercontent.com/czah7/paws-academy-updates/main/update.json`. APKs are immutable assets on public GitHub releases in `czah7/paws-academy-updates`; the manifest is updated only after an uploaded APK and its SHA-256 have been verified.

Release order: export a signed Android APK; test that exact artifact; calculate SHA-256; upload the APK; update manifest URL/hash/notes; verify both over HTTPS; commit; tag; push. Never point the manifest at an unvalidated artifact. Android installation additionally needs a FileProvider/plugin or platform bridge plus `REQUEST_INSTALL_PACKAGES`; the current prototype implements manifest/build checks and hashing but does not claim installer completion.

The permanent release keystore and passwords must never be committed. Losing this signing identity prevents Android from installing future Paws Academy releases over the existing app. Keep multiple encrypted backups outside the repository.

Build the production APK with `tools/build_release_interactive.ps1`. It requests the password securely, passes it to Godot through the documented `GODOT_ANDROID_KEYSTORE_RELEASE_PASSWORD` process environment variable, and clears it after export. The password is never written to the repository.
