# dotsu-ota-v2

This repository hosts release assets for Dotsu native OTA updates.

## Manifest

`manifests/ios.json` and `manifests/android.json` are the small client-facing indexes for OTA updates. Native apps should fetch the file for their platform, look up `versions[appVersion]`, compare `otaVersion` against the locally installed OTA version, and download `downloadUrl` only when the manifest version is newer.

Current production URLs after these files are merged to `main`:

```text
https://raw.githubusercontent.com/kotoba-tech/dotsu-ota-v2/main/manifests/ios.json
https://raw.githubusercontent.com/kotoba-tech/dotsu-ota-v2/main/manifests/android.json
```

## Updating The Manifest

Update the matching platform and app version entry every time an OTA release is published:

- `otaVersion` and `releaseId` should be the GitHub release id. The app uses this as the installed OTA version.
- `releaseTag`, `releaseName`, and `publishedAt` should match the release that introduced the platform-specific asset.
- `assetId`, `assetName`, `assetSize`, and `downloadUrl` should match the uploaded zip asset.
- Use the platform-specific manifest file for each entry. For example, an Android OTA deploy should update `manifests/android.json`, but it should not bump iOS just because the iOS asset was carried forward into the newer release.

`manifest.schema.json` documents the expected shape of each platform manifest and can be used by deploy automation to validate updates before publishing.