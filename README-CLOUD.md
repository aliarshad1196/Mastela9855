# Build Mastela 9855 without owning a Mac

This project is prepared for cloud iOS CI using Codemagic.

## Required

- Apple Developer Program membership
- App Store Connect access
- A GitHub account/repository
- Codemagic account

## 1. Upload this project to GitHub

Create a new GitHub repository and upload the contents of this folder. The repository root must contain:

- `Mastela9855.xcodeproj`
- `Mastela9855/`
- `codemagic.yaml`

## 2. Create the Apple App Store Connect integration

In Codemagic, connect the Apple Developer Portal/App Store Connect account and create an integration named:

`mastela_appstore_connect`

The integration must have permission to create/use signing credentials and upload builds.

## 3. Create the app record

In App Store Connect create an iOS app with bundle ID:

`com.local.Mastela9855`

If this bundle ID is already taken, change it in both the Xcode project and `codemagic.yaml` before building.

## 4. Add the GitHub repository to Codemagic

Choose the repository, select the `mastela-ios-testflight` workflow from `codemagic.yaml`, and start the build.

Codemagic will build/sign the IPA on a cloud Mac and upload it to TestFlight.

## Important

The Volume Level 1/2/3 implementation is currently marked as a protocol inference from the recovered factory-key mapping. It should be tested against the actual swing before treating the volume commands as confirmed.
