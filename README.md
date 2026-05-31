# dotsu-ota-v2

This repository hosts release assets for Dotsu native OTA updates.

## Manifest

`manifest.json` is the small client-facing index for OTA updates. Native apps should fetch this file, look up `platforms[platform][appVersion]`, compare `otaVersion` against the locally installed OTA version, and download `downloadUrl` only when the manifest version is newer.

Current production URL after this file is merged to `main`:

```text
https://raw.githubusercontent.com/kotoba-tech/dotsu-ota-v2/main/manifest.json
```

## Updating The Manifest

Update the matching platform and app version entry every time an OTA release is published:

- `otaVersion` and `releaseId` should be the GitHub release id. The app uses this as the installed OTA version.
- `releaseTag`, `releaseName`, and `publishedAt` should match the release that introduced the platform-specific asset.
- `assetId`, `assetName`, `assetSize`, and `downloadUrl` should match the uploaded zip asset.
- Use the platform-specific release for each entry. For example, an Android OTA deploy should update the Android entry, but it should not bump the iOS `otaVersion` just because the iOS asset was carried forward into the newer release.

`manifest.schema.json` documents the expected shape and can be used by deploy automation to validate updates before publishing.