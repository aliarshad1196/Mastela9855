# Mastela 9855 iOS Controller

A native SwiftUI/CoreBluetooth controller for the Mastela 9855 swing.

## Important

The BLE UUIDs and command protocol in this project were recovered from the supplied Mastela APK source:

- Service: `03B80E5A-EDE8-4B33-A751-6CE34EC4C700`
- Write/notify characteristic: `7772E5DB-3868-4112-A1A9-F2669D106BF3`

The original app searches for BLE devices whose advertised `name` or `localName` contains `swing`, connects to the above service/characteristic, enables notifications, then requests status.

## Known commands recovered from the original app

Commands are five bytes and begin with ASCII `cmd` (`63 6D 64`).

Swing:
- Level 1: `63 6D 64 31 31`
- Level 2: `63 6D 64 31 32`
- Level 3: `63 6D 64 31 33`
- Level 4: `63 6D 64 31 34`
- Level 5: `63 6D 64 31 35`
- Swing off: `63 6D 64 31 39`

Music:
- On: `63 6D 64 32 38`
- Off: `63 6D 64 32 33`

Timer:
- 15 min: `63 6D 64 30 31`
- 30 min: `63 6D 64 30 32`
- 45 min: `63 6D 64 30 33`
- Off: `63 6D 64 30 39`

Power:
- On: `63 6D 64 33 35`
- Off: `63 6D 64 33 36`

Status request:
- `63 6D 64 33 38`

The original app also contains a separate six-byte `onPowerOnOff` command (`69 96 03 01 0A XX`), but the main-screen power logic uses `cmd35`/`cmd36`; the project therefore uses the latter.

## Status notifications

The original app treats a notification beginning with byte 0 == `0` as a status packet:

- byte 1: power state
- byte 2: swing level
- byte 3: music state
- byte 4: timer state

## Build

This project requires macOS + Xcode because Apple does not provide Xcode/iOS device signing on Windows.

1. Create a new iOS App in Xcode named `Mastela9855` using SwiftUI.
2. Replace the generated Swift files with the files in this folder, or add these files to an existing Xcode project.
3. Add `Info.plist` entries if Xcode manages the plist automatically.
4. Select an iPhone target.
5. Enable a valid Apple Development Team under Signing & Capabilities.
6. Build and run on the iPhone.
7. Grant Bluetooth permission.
8. Power on the Mastela swing.
9. Tap Scan & Connect.

For a first test, keep the phone close to the swing and leave the official Mastela app disconnected so only this app is communicating with it.

## Notes

The app deliberately does not attempt to clone the original UI. It provides a clean controller plus an Advanced raw-hex panel for protocol testing.

The supplied source did not expose a clearly named "volume" control; if the 9855's volume is controlled by one of the numbered/key commands, the next step is to map those commands from the original key screen and add explicit Volume +/- controls.
