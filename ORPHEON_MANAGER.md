# Orpheon Manager

Orpheon Manager is a GPL-3.0 Android APK patch manager derived from ReVanced
Manager. It is intended to apply a narrowly scoped, version-locked export patch
to a user-supplied Orpheon APK, then sign and install the resulting APK.

## Intended update flow

1. Download a regular (non-split) Orpheon APK from the upstream GitHub release.
2. Open Orpheon Manager and select the downloaded APK from storage.
3. Select the Orpheon Export patch bundle that supports that exact version.
4. Patch and install the generated APK.
5. For every later update, use the same local keystore and repeat the process.

The local keystore is deliberately persistent: changing or deleting it means
Android cannot install later patched releases over an existing patched build.

## Patch-bundle policy

Patches belong in a separately versioned `.rvp` bundle. The manager must reject
an APK whose package name or version is not explicitly supported by the bundle.
Do not disable compatibility checks: an output APK which installs but crashes is
not an acceptable update path.

The export patch must write clear audio through Android's MediaStore (for example
to `Music/Orpheon`) from Orpheon's own decrypting code. It must never try to read
another app's private storage or bypass Android's application sandbox.

## Licensing and credit

This app includes and modifies GPL-3.0 ReVanced Manager code. Orpheon itself is
GPL-3.0. Any distributed build, patch bundle, and derivative source must retain
the relevant notices and be published under GPL-3.0 with corresponding source.
