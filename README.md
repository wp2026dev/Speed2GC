# Speed2GC

**Your Speediance workouts in Garmin Connect.**

Speed2GC is an Android app that transfers your Speediance workouts to Garmin Connect as FIT activities. You can also download FIT files and import existing FIT files manually.

**Status: Beta.** Features and data transfers are still being tested and improved. Read the notes for each version and check your first transferred activities in Garmin Connect.

## Download the APK

Approved APK versions are distributed through **[Releases](https://github.com/wp2026dev/Speed2GC/releases)**.

Open the release you want and download `Speed2GC-<version>.apk` from **Assets**. Beta versions are marked as **Pre-release**. Each release includes its changes, known limitations and, where provided, SHA-256 checksums.

## Features

- Speediance as the workout source and Garmin Connect as the destination.
- Manual workout transfers to Garmin Connect.
- Optional synchronization on app launch and in the background.
- FIT export without uploading to Garmin Connect.
- Manual import of one or more FIT files.
- Transfer history and local records of activities already transferred.
- Configurable activity limit, weight unit and workout time zone.
- German and English interfaces with built-in help.

## Requirements

- Android **8.0 or later**.
- A Garmin Connect account for uploads.
- A Speediance account to retrieve Speediance workouts.
- Internet access for sign-in and synchronization.
- Folder access permission for FIT exports.

## Installation and updates

1. Download the APK from a release.
2. Open it on your Android device.
3. If prompted, allow your browser or file manager to install apps from this source. The setting's name may vary by device.
4. Confirm the installation and open Speed2GC.

To update, install the new APK **over your existing Speed2GC installation**. Do not uninstall the app first if you want to retain local settings and transfer records.

Speed2GC is a separate app and can be installed alongside the earlier GarminSync app. Sign-ins, settings and local transfer records are not automatically migrated from GarminSync.

## Initial setup

1. Open **Settings** using the gear icon on the home screen.
2. Sign in to **Garmin Connect**.
3. Sign in in the **Speediance** section and enable Speediance.
4. Check your weight unit and workout time zone.
5. Set the number of activities to check. The default is the latest **25** completed activities; the limit can be adjusted from **1 to 100**.
6. Select **Start sync** to begin the transfer.

For automatic runs, enable both the relevant main switches under **Synchronization** and the corresponding Speediance options. Android may delay background runs.

## FIT export and manual import

The default export folder is **`Download/Speed2GC`**. Select the folder in Settings and grant access. If it does not exist, create it in the Android file picker.

- **Download FIT files:** Saves Speediance activities to the selected folder without uploading them to Garmin Connect.
- **Import FIT files:** Opens the file picker. After the files have been checked, confirm the Garmin upload with **Upload files**.

## Important beta notes

- Activities already transferred successfully are skipped based on local records. Duplicate checks also consider identical FIT files. Different files representing the same workout can still create duplicates, particularly when using multiple import apps.
- If an upload result is uncertain, check Garmin Connect and the transfer history before transferring the activity again.
- Differences between total and lap times for Ski activities are still being investigated. Stroke counts are currently unavailable.
- The optional derived heart-rate chart uses available maximum heart rates recorded for sets. It is not a continuous heart-rate measurement.
- Changes to Speediance or Garmin services may affect sign-in and transfers.

See each release's notes for version-specific limitations and the checks actually performed.

## Report an issue

Please report problems through **[Issues](https://github.com/wp2026dev/Speed2GC/issues)** and include, where possible:

- App version, device model and Android version.
- Steps to reproduce the problem.
- Expected and actual behavior.
- The error message and, if relevant, a reviewed excerpt from the debug log.

The debug log is available in Settings. **Do not publish passwords, session tokens or personal workout data.** Review screenshots and logs before uploading them.

## About this repository

This repository distributes approved APKs and public release information. The app's source code is maintained privately.

Speed2GC is an independent project. It is not affiliated with or endorsed by Garmin or Speediance. Product names and trademarks belong to their respective owners.
