# Speed2GC

**Your Speediance workouts in Garmin Connect.**

Speed2GC is an Android app that transfers Speediance workouts to Garmin Connect as FIT activities. It also exports FIT files without a Garmin upload and imports existing FIT files into Garmin Connect.

**Status: Beta.** Check your first transferred activities in Garmin Connect and read the notes for the APK version you install.

## Download and install

Download an APK from [Releases](https://github.com/wp2026dev/Speed2GC/releases). Open the release and select `Speed2GC-<version>.apk` under **Assets**. Beta releases are marked **Pre-release**.

Android **8.0 or later** is required. Allow your browser or file manager to install the APK if Android prompts you. For updates, install over the existing Speed2GC app to retain settings and local transfer records.

The earlier GarminSync app has separate sign-ins, settings and transfer records; these are not automatically migrated.

## Setup and synchronization

1. Open **Settings** using the gear icon.
2. Sign in to Speediance and Garmin Connect.
3. Check the Speediance region, detected or manually selected weight unit, and workout time zone.
4. Set the activity count: **1–100**, default **25** recent completed activities.
5. Return to Home and select **Start sync** (**Synchronisieren** in German).

Speediance is the workout source. A Garmin sign-in is needed for Garmin uploads, but not for local FIT exports or diagnostic packages. Internet access is required to retrieve workouts and contact the services.

Automatic background sync is optional. Enable it under Synchronization and keep Speediance's background participation enabled. Android controls execution timing and may delay runs. Opening the app does not trigger a separate app-launch sync; a due background job can run while the app is open. Current Garmin sync progress and Stop are shown on Home.

### Planned interface update (S2GC-0099)

The following changes are planned and are **not included in 0.1.31-beta**. Check future APK release notes before following these locations:

- **Reset sync status** will move into **Settings → Synchronization**. It will appear only after a fully successful sync, including a run where all activities were already present. A failed or cancelled first sync, FIT export or diagnostic export will not reveal it. After resetting, it will remain hidden until another successful sync.
- After confirmation, resetting clears local upload records, saved source results and the last successful sync time, and discards pending file selections and internal queue files. History, sign-ins, settings, exported FIT files and the technical log remain. Garmin activities are not deleted. Check Garmin before allowing another sync because differently generated files can cause duplicates.
- **View log** will show a red **Clear log** button directly in the log view, without an additional card. Clearing removes local logs, not history, synchronization records or saved diagnostic packages. New entries can appear while Diagnostic mode remains enabled; disable the mode to stop further logging.

## FIT export and import

- **Export FIT files:** Saves Speediance activities to a folder you select in Settings, without uploading to Garmin. There is no mandatory default export folder. Grant folder access in the Android picker.
- **Import FIT files:** Select local FIT files, review the result and confirm the Garmin upload.

Changing or removing folder access does not delete exported files. The app preserves Speediance's original workout/exercise names in new FIT files. Garmin may display its own localized exercise names based on numeric exercise mappings. Some mappings are general approximations rather than exact variants.

## Report a beta problem

Create an [issue](https://github.com/wp2026dev/Speed2GC/issues) and include:

- App version, Android version and device model.
- Steps to reproduce the problem.
- Expected and actual behavior, including the error message.
- The affected workout date/type where relevant, without unnecessary personal information.

### Create a diagnostic package

These instructions apply to **0.1.31-beta and later versions that include Diagnostics**; check the APK's release notes for availability.

1. Open **Settings → Diagnostics** (**Einstellungen → Diagnose**).
2. Enable **Diagnostic mode** if it is off. With no saved preference it defaults to on; your explicit choice is retained.
3. Reproduce the problem where possible. Enabling diagnostics cannot recover older missing log events.
4. Select **Create diagnostic package** (**Diagnosepaket erstellen**), then **Create and save**.
5. Choose where to save the ZIP using the Android file dialog.

The package contains retrieved Speediance workout JSON, related newly generated FIT files, a snapshot of the current/rotated technical log, export settings and file mappings/checksums. It uses the configured activity count. It does not upload to Garmin or reset synchronization records. These newly generated files are not necessarily identical to a previous upload.

**The ZIP contains personal workout data and is not anonymous. Do not attach it or a public download link to a public GitHub issue.** Credentials and authentication headers are excluded, but review the contents before sharing.

If package creation fails, include the visible error message in your issue. Do not reset sync records as a troubleshooting step.

**View log** opens the local protocol and lets you clear it. Disabling Diagnostic mode stops new logging and hides both diagnostic actions; existing logs are retained. Packages are created only manually and are never sent automatically. Delete externally saved ZIPs separately when no longer needed.

## Beta limitations and transfer safety

- Local transfer records and FIT checksums help avoid repeated uploads. Different files representing the same workout can still create duplicates, especially across multiple apps.
- If an upload result is uncertain, check Garmin Connect and History before trying again. Deleting a Garmin activity does not automatically reset Speed2GC's local records.
- Existing Garmin activities are not retroactively corrected by an app update.
- General exercise mappings may not preserve the exact Speediance variant. Within-set weight changes are currently reduced to one weight per exported set, and a separate left/right marker is not always retained.
- Derived heart rate is an approximation from available set maxima, not a continuous sensor measurement.
- Ski timing differences remain under investigation; stroke counts are not currently exported.
- Speediance/Garmin service changes can affect sign-in and transfers. Automated tests do not replace a device or live Garmin check.

## About this repository

This repository distributes APKs and public release information and collects beta feedback. The app source is maintained privately. The maintainer publishes APKs manually.

Speed2GC is independent and is not affiliated with or endorsed by Garmin or Speediance. Product names and trademarks belong to their respective owners.
