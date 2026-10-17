# Speed2GC

**Your Speediance workouts in Garmin Connect.**

Speed2GC is an Android app for transferring Speediance workouts to Garmin Connect as FIT activities. It also lets you export workouts as FIT files and upload existing FIT files to Garmin Connect.

Speed2GC is in beta. Check transferred activities in Garmin Connect and report unexpected results with the app version and a description of what happened. A diagnostic package can help investigate problems.

## Installation

- Requires **Android 8.0 or later**.
- Download an APK from [Releases](https://github.com/wp2026dev/Speed2GC/releases) and open it on your Android device.
- Allow installation from your browser or file manager if Android asks.
- Install updates over the existing Speed2GC installation to retain its settings, sign-ins and synchronization records.

## Connect your accounts

Open **Settings** using the gear icon and connect Speediance and Garmin Connect.

Check the Speediance region, workout time zone and weight unit. If the app cannot detect the unit, select **kg** or **lb** to match your Speediance data. Complete any additional Garmin sign-in or verification steps shown by the app.

Connection indicators show:

| Color | Meaning |
|---|---|
| Green | Signed in; Speediance's weight unit is also available. |
| Orange | Speediance is signed in, but its weight unit needs attention. |
| Red | Not signed in or the session has expired. |

Tap a connection indicator or its status text to open the corresponding settings. A green indicator reflects the stored connection state; a later server request can still fail.

Garmin sign-in is required for synchronization and FIT imports. FIT exports and diagnostic packages require Speediance access but do not require Garmin sign-in.

## Synchronize workouts

Select **Start sync** (**Synchronisieren** in German) on Home. Speed2GC retrieves recent Speediance workouts, prepares FIT activities and checks for existing transfers before uploading them to Garmin Connect.

The Speediance activity count can be set from **1 to 100**, with **25** as the default. This is the number of recent source workouts to examine, including workouts already transferred. It does not mean that 25 new workouts will be uploaded. Workouts outside that selection are not automatically included.

Progress appears on Home. When the current phase has a known scope, the bar shows completed items out of the total. Otherwise, it uses an indeterminate animation. Each phase has its own progress; completing a phase does not by itself confirm a successful upload.

**Stop** requests a safe cancellation. An upload already in progress may need to finish before the operation stops. Confirmed uploads are retained. Home also shows the last fully successful synchronization for the connected Garmin account; a run containing only already-present activities can be successful.

### Background synchronization

Enable **Automatic background sync** under **Settings → Synchronization**, then choose an interval and whether an unmetered network is required.

Both accounts must be connected, and Speediance's weight unit must be available. Missing sign-ins prevent transfer. Android controls background execution and can delay or skip a scheduled run, for example because of network availability or battery restrictions.

Some temporary problems before the upload phase can lead to up to three additional attempts. An unclear upload result is not automatically resent. Opening the app does not start a separate app-launch synchronization, although a due background job can run while the app is open.

### Conversion and duplicate checks

Review the conversion settings before transferring workouts. Weight interpretation and workout time zone should match your Speediance data. For strength-training grouping, choose whether workouts are combined and the allowed gap between them. Optional heart-rate conversion uses source data; it does not add a new sensor measurement.

Where grouping is enabled, several workouts can form one FIT activity. A preserved group remains a single transfer unit. Exercise names are exported as supplied by Speediance; Garmin's exercise names and presentation can differ.

The result depends on the data Speediance provides and what Garmin supports. Some fields or totals can appear differently in the two services.

Duplicate protection uses stored transfer records and checks against Garmin. Creating a different FIT file for the same workout can still produce a duplicate. If an outcome is unclear, check Garmin before allowing another transfer.

## Export FIT files

Select **Export FIT files** on Home to create FIT files from Speediance workouts and save them in the selected export folder. Choose or change that folder in Settings and grant the requested Android file access.

The source activity count and conversion settings determine the export scope. Exporting does not upload anything to Garmin.

Pay attention to the result message. A failed or interrupted export can require checking the destination folder, especially if a file could not be restored or removed. A saved file and a confirmed Garmin upload are separate results.

## Import FIT files

Select **Import FIT files** on Home and choose existing FIT files using the Android file picker. Review the validation results and confirm the upload.

A selection can contain up to **100 files**. The app also applies file-size and total-selection limits; these are separate from the Speediance activity-count setting.

Already imported, repeated, invalid or unresolved files are identified before transfer. Garmin sign-in is required. Check the individual results after importing; a partially completed selection does not mean that every file was uploaded.

## History and transfer details

History records:

- Manual synchronization.
- Background synchronization.
- FIT export.
- Confirmed FIT import operations.
- Synchronization-status resets.

Events show a successful, partially successful or failed result. Cancelled, skipped and unclear outcomes are identified in the details.

Tap an event to see its results and affected workouts or files. Tap an individual entry for more information and any available actions. Older records or interrupted retrievals may not contain a complete workout or file list; missing information is indicated.

The toolbar provides refresh, filters, sort order and deletion. Filters cover event type, period and result. Sort switches between newest first and oldest first, with newest first as the default.

Deleting History removes its displayed events and associated event details across accounts, including entries hidden by filters. It does not remove Garmin activities, synchronization proofs, queued transfers or the technical log.

### Reconsider a transfer

**Reconsider on next sync** is available for eligible transfers in their details. Confirming it queues a transfer for checking during a subsequent synchronization; it does not upload immediately or delete anything from Garmin.

Check uncertain uploads in Garmin first and use **Check status** where available. Existing merged groups cannot be split into separate retries. If the original FIT file or matching source data is missing, the transfer remains pending and the app explains what is needed.

Queued transfers remain accessible after History is cleared. Their processing still requires the appropriate connected accounts and source data.

### Reset synchronization status

**Reset sync status** is in the Synchronization settings. It becomes available after a fully successful synchronization has been recorded for the currently connected Garmin account.

After confirmation, the app clears local synchronization records across accounts, queued reconsiderations and pending file selections. The next sync examines activities within the configured source selection again. History, sign-ins, settings, exported files and Garmin activities remain.

This is a broad reset. For an individual workout, prefer its available History actions and check Garmin first to avoid duplicates.

## Diagnostics and beta feedback

The **DIAGNOSTICS** card in Settings contains **Diagnostic mode**, **View log** and **Create diagnostic package**.

Diagnostic mode is enabled when no preference has been saved. Your choice is retained. Disabling it stops new technical logging and hides the diagnostic buttons; it does not delete the existing log. Functional History remains available independently of this setting.

**View log** opens the technical text log. Its toolbar provides refresh, filtering, sorting and deletion. Filters include period, component, text search and error indications. Filters affect the display; diagnostic packages contain the complete stored log. Deleting the log does not delete History or synchronization records.

### Create a diagnostic package

Use **Create diagnostic package** when investigating a problem or preparing a beta report. The app retrieves Speediance workout data within the configured activity count and creates a ZIP containing:

- Safely redacted source-data responses.
- FIT files generated from those workouts.
- The technical log.
- Information about the included files and export settings.

Choose the destination in the Android file dialog. The filename includes the installed Speed2GC version and a timestamp. Package creation does not upload activities to Garmin or reset synchronization records.

The package contains **personal workout data** and is **not anonymous**. Credentials and authentication headers are excluded. Nothing is sent automatically. Review the contents before sharing.

An explicitly incomplete package may be produced if retrieval or processing fails. Its manifest identifies missing parts. Cancellation or storage problems can prevent package creation. Pay attention to whether the saved package could be verified at its destination.

For useful feedback, include the app version, what you expected, what actually happened and the steps that reproduce the problem. A diagnostic package can provide additional evidence.

## Settings, help and project information

Settings include language and appearance options. German and English are available, and the app supports light, dark and system appearance.

Offline Help explains the controls and settings. **ABOUT** contains the installed version, App info, Privacy, Licenses and a link to the [GitHub project](https://github.com/wp2026dev/Speed2GC).

Garmin and Speediance services require a working connection and valid sign-ins. Service-side changes, incomplete source data or interrupted transfers can affect results. Check History and the available diagnostic information when something does not work as expected.
