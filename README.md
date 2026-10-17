# Speed2GC

**Your Speediance workouts in Garmin Connect.**

Speed2GC is an Android app that transfers Speediance workouts to Garmin Connect as FIT activities. You can also export workouts as FIT files without uploading to Garmin, or import existing FIT files into Garmin Connect.

**Documentation: 0.1.45-beta · Android 8.0 or later · Updated October 17, 2026.**

This README describes the current development version. Check [Releases](https://github.com/wp2026dev/Speed2GC/releases) for the APKs actually published. Speed2GC is in beta: review transferred activities in Garmin Connect, especially after an update.

## Download and install

1. Open [Releases](https://github.com/wp2026dev/Speed2GC/releases).
2. Select a release and download `Speed2GC-<version>.apk` under **Assets**.
3. Allow installation from your browser or file manager if Android asks, then open the APK.

Install updates over the existing Speed2GC app to retain settings, sign-ins and local synchronization records. The earlier GarminSync app has separate data that is not automatically migrated.

## Connect and synchronize

1. Open **Settings** using the gear icon.
2. Sign in to Speediance and Garmin Connect.
3. Check your Speediance region, weight unit and workout time zone. If the unit is not detected, select **kg** or **lb** to match your source data.
4. Set how many recent completed activities to retrieve: **1–100**, with **25** as the default.
5. Return to Home and select **Start sync** (**Synchronisieren** in German).

Speediance is the workout source; Garmin Connect is the upload destination. A Garmin sign-in is required for synchronization and manual FIT imports. Local FIT exports and diagnostic packages require Speediance access, but no Garmin sign-in.

Connection indicators show the stored sign-in state. Speediance also indicates whether its weight unit is ready. A green indicator does not guarantee that every subsequent server request will succeed.

Current synchronization progress and **Stop** appear only on Home. The bar fills according to completed/total items in the current phase when its scope is known; otherwise it uses an indeterminate animation. Each phase starts its own progress. Processing all items does not imply successful uploads. No duration is guessed. Stop requests a safe cancellation; an upload already in progress may need to finish first. Home also shows the last fully successful synchronization for the currently connected Garmin account. A run containing only activities already present in Garmin can count as successful.

### Background synchronization

Enable **Automatic background sync** under **Settings → Synchronization**. There is one global switch; Speediance has no separate background-participation switch.

Choose an interval and, optionally, require an unmetered network. Both services must be signed in and the Speediance weight unit must be known. Android controls execution timing and may delay or skip runs. Opening the app does not start a separate app-launch synchronization; a due background job can still run while the app is open.

Suitable temporary obstacles before the upload phase can schedule up to **three additional attempts**, targeting delays of **5, 15 and 30 minutes**. These times are not guaranteed. Missing sign-in, an unknown unit, intentional cancellation and uncertain upload results do not trigger blind retries. Disabling background synchronization cancels scheduled retries.

### Speediance retrieval errors

History pages are read with short, cancellable pauses. If Speediance returns API code **2001** in an HTTP-success response, the app can retry the same read-only history page once after a short pause. The retry budget applies to the whole retrieval, rather than resetting on every page.

This does not sign in again or repeat a Garmin upload. Empty years do not prematurely stop the search for older workouts. Persistent retrieval errors remain errors. This handling does not establish an official meaning or a confirmed server-side cause for code 2001.

## FIT export and import

| Action | Direction | Behavior |
|---|---|---|
| **Export FIT files** | Speediance → local FIT files | The Speediance icon identifies the source. Select an export folder and grant access through Android's folder picker. No Garmin upload is performed. |
| **Import FIT files** | Local FIT files → Garmin Connect | The Garmin icon identifies the destination. Select files, review validation results and confirm the upload. Selecting files alone does not upload them. |

There is no mandatory default export folder. Use Select export folder to change the destination; the former Remove export folder option is no longer shown. Failed exports attempt to restore the previous folder state; incomplete restoration or cleanup is reported.

Each import selection supports up to **100 distinct files**, **100 MiB per file** and **250 MiB total**. Actual bytes are checked even if file-size metadata is unavailable or inaccurate. Cancellation is checked between copy blocks, although a blocking document provider can delay it. Fully validated files remain selected; unfinished copies are discarded.

Speediance's original workout and exercise names are preserved in FIT files. Garmin may display localized exercise names using numeric exercise mappings. Some mappings use a general exercise rather than an exact variant.

## History

Open **History** (**Verlauf**) on Home. The fixed toolbar stays visible while the entries scroll:

**Refresh → Filters → Sort → Delete**

- **Refresh** reloads local entries while retaining filters and sort order.
- **Filters** combines event type, date range and result. Dates include all time, today, the last 7 or 30 calendar days including today, or an inclusive custom From/To range in your local time zone. The filter button shows the number of active filters.
- **Sort** switches directly between **Newest first** and **Oldest first**, without a submenu. Newest first is the default. Older pages follow the selected direction.
- **Delete** requires confirmation and hides the entire visible history for all accounts, including filtered-out entries. Synchronization records used to prevent duplicate uploads and the technical log remain.

Recorded event types are manual synchronization, background synchronization, FIT file export, confirmed FIT file import and resetting synchronization status.

Each card has two lines: local date/time followed by the **action in bold**, then a single-line result summary. Tap anywhere on a card to open its dedicated detail page with overview, results, reasons and stored linked uploads. The status-colored **i** icon is centered on the left; the entire card is one accessible action. Events and individual workout/file entries share compact padding and equal-size left info icons; the whole individual entry also opens its details. Back returns to the same History filters, sort order and position. Start, end, duration and available retry/grouping/reason information appear immediately below the status, without expanding a separate section; necessary error guidance remains visible. Workouts/files are the main content, with individual results and separate item details. Reconsider on next sync appears below eligible lists; per-item actions live directly below the information in item details, without an extra status card or repeated success confirmation. Changed verification results and necessary queue/error guidance remain visible.

| Result | Indicator | Meaning |
|---|---|---|
| Successful | Green | The operation completed successfully. |
| Partially successful | Orange | Some results were confirmed, but other steps failed, were cancelled or remain uncertain. |
| Failed | Red | The operation did not complete successfully and has no confirmed successful portion. |

Status is also shown as text. Skipped background attempts, cancellation, interruptions and uncertain upload results retain an explicit explanation. Check uncertain uploads in Garmin before allowing another transfer.

**No entries** means the history is empty. **No matching entries** means existing entries were excluded by active filters. Delete is gray and disabled for an empty unfiltered history; filtering out existing entries does not disable it.

Account-bound events remain separated by Garmin account. Exports made without a Garmin account and global reset events are shown without assigning them to another account. Older standalone uploads without a recorded event type appear under **Older transfers**, only when matching entries exist. Historical exports or resets cannot be reconstructed retroactively.

Observed skipped background attempts include their reason. Similar skipped events may be grouped within 24 hours. Skipped entries without linked uploads are cleaned up during app use after 30 days or above 500 entries per account. Other event records have no new automatic deletion period. Jobs never started by Android cannot be recorded. Functional history remains active when Diagnostic mode is off.

For new operations, local per-event snapshots include actually observed workouts/files, original names, workout times, available training summaries, merged groups and individual results, including already-present and unprocessed items. Transfer and workout counts are distinguished. Export records distinguish planned names from provider-reported destination names and confirmed saves from rolled-back or uncertain writes. Reset events list the affected status areas.

Older events may have incomplete lists and are explicitly marked. Early retrieval failures cannot produce a complete list of unknown workouts. Original event outcomes stay separate from the current upload-proof/queued status. These records are independent of Diagnostic mode and cannot authorize an upload. Clearing History also deletes the additional content snapshots while retaining duplicate/uncertainty proofs and queued transfers.

### Reconsider selected transfers

Open an event's details and select **Reconsider on next sync** (**Erneut berücksichtigen**). Select the transfers to queue and confirm. Identical FIT hashes count once; merged workouts remain one indivisible transfer group. Uncertain uploads must be checked and explicitly resolved first.

This preserves the historical result and queues a local, account-bound check. It does **not** immediately upload or delete anything in Garmin. Available original FIT files are validated and retained. The next permitted sync checks queued originals even outside the normal Speediance activity limit, reconciles Garmin first and uploads only when safe. A failed reconciliation does not trigger an upload; an uncertain outcome stays blocked. Normal sync sign-in and unit requirements still apply.

If an original is missing, the record stays pending: use **Supply original FIT** or increase the source read limit if the full original workout/group remains available. Only an identical file or verified identical reconstruction is accepted. Missing or changed data is never reported as successfully retried. Open **Queued transfers** in History to inspect pending cases, including after clearing History.

Up to 100 pending transfers per Garmin account can be queued; retained copies are limited to 250 MiB in total and 100 MiB per file. They contain personal workout data and remain private to the app. Completed copies may remain for later checks until global sync reset, clearing app data or uninstalling. Global reset removes queued records and retained copies as well.

### Reset synchronization status

**Reset sync status** is in **Settings → Synchronization**. It appears after a fully successful synchronization has been recorded for the currently connected Garmin account. FIT imports, FIT exports and diagnostic exports do not set that timestamp.

After confirmation, the reset removes active local upload proofs, saved source results and successful-sync timestamps for all affected accounts, and discards pending selections, queued reconsiderations and internal queue files. History, sign-ins, settings, exported FIT files and the technical log remain. Garmin activities are not deleted. The button stays hidden until another successful synchronization.

Check Garmin first: resetting records can allow another upload, and differently generated FIT files for the same workout can create duplicates. For one activity, prefer the appropriate check or permission action in its history details.

## About

Settings → ABOUT shows the installed version and App info, Privacy and Licenses. An outlined, unfilled info icon is centered beside the compact two-line version/link block, without an extra blank row below the links. Project on GitHub below uses a matching-size GitHub icon and opens the repository externally for information, downloads and issue reporting. Nothing is automatically reported or attached. In beta builds App info includes a short beta notice welcoming feedback.

## Report a beta problem

Create an [issue](https://github.com/wp2026dev/Speed2GC/issues) and include:

- Speed2GC version, Android version and device model.
- Steps to reproduce the problem.
- Expected and actual behavior, including the exact visible error or code.
- Whether the problem happens every time, only on the first attempt or only in the background.
- The affected workout date/type when relevant, without unnecessary personal information.
- Whether a diagnostic package could be created; if not, the error shown while creating it.

**For synchronization, import or export problems, create a diagnostic package soon after reproducing the issue.** It includes the technical log needed to investigate the sequence of events. Keep Diagnostic mode enabled during reproduction and do not clear the log or reset synchronization records as a troubleshooting step.

### Diagnostics and the text log

The **Diagnostics** card is in Settings directly above **About**. **Diagnostic mode** is enabled when no preference has been saved. Your explicit choice is retained after restarting or updating.

**View log** opens the local technical log as text. It uses the same fixed **Refresh → Filters → Sort → Delete** toolbar as History. Available filters are:

- **Period:** local date range.
- **Area:** Speediance, Garmin, synchronization, FIT import/export, background scheduling, diagnostics or app/other.
- **Text search:** case-insensitive matching, such as an HTTP code or exception class.
- **Only error indications:** recognized error markers, not a complete stored severity classification.

Sort switches directly between newest and oldest first. Recognized error/stack blocks keep their internal order. Filtering happens before the display limit, and truncated output is marked. Display filters and sorting do not change stored log files or the complete original log included in a diagnostic package.

The view distinguishes an empty log from entries excluded by filters. Delete is gray and disabled for an empty log. Deleting requires confirmation and clears the entire technical log, including filtered-out lines, while retaining history, synchronization records and saved diagnostic packages. New log entries may appear while Diagnostic mode remains enabled.

Disabling Diagnostic mode stops new technical logging and hides **View log** and **Create diagnostic package**. Existing logs remain. Workout JSON is collected only when you manually create a package.

### Create a diagnostic package

1. Open **Settings → Diagnostics** (**Einstellungen → Diagnose**).
2. Enable **Diagnostic mode** if necessary and reproduce the problem where possible. Missing older log events cannot be recovered.
3. Select **Create diagnostic package** (**Diagnosepaket erstellen**), then **Create and save**.
4. Choose where to save the ZIP using the Android file dialog.

The suggested filename includes the installed app version, for example:

`Speed2GC-0.1.45-beta-Diagnose-20261016-203229.zip`

The package includes safely redacted Speediance workout responses, related newly generated FIT files, a snapshot of the current and rotated technical log, export settings and file mappings/checksums. It uses the configured activity count, although retrieved history responses can contain additional records. It does not upload to Garmin or reset synchronization records.

Creating a package retrieves Speediance data again. Its responses and newly generated FITs are not necessarily identical to those from the earlier failed synchronization or a previous upload.

If retrieval or processing fails, the app may still save an explicitly **incomplete package** containing already safely captured responses, valid FITs and the log. The manifest identifies missing parts and the failure phase. Missing data is not reconstructed. Cancellation and disabling diagnostics still cancel the export; storage or size errors may prevent even an incomplete package.

After saving, the app reads back the destination ZIP and compares it with the internal file. If the document provider prevents verification, the app reports **saved, but not verifiable**. Different bytes produce an error. A failed destination that the provider cannot delete may need manual removal.

**Diagnostic packages contain personal workout data and are not anonymous. Do not attach the ZIP or public download links to public GitHub issues.** Known credential and account fields are redacted, but this is not full anonymization. Review contents before sharing.

Nothing is sent automatically. Delete saved ZIPs separately when no longer needed. Clearing the log, signing out or uninstalling does not remove externally saved packages.

## Beta limitations and transfer safety

- Local upload records, file hashes and Garmin checks help avoid repeated uploads. Different files for the same workout can still create duplicates, especially across apps.
- If an upload result is uncertain, check Garmin and History before allowing another transfer. Deleting an activity in Garmin does not automatically reset Speed2GC's local records.
- Existing Garmin activities are not retroactively corrected by an app update.
- General exercise mappings may not preserve an exact variant. Within-set weight changes are reduced to one exported weight per set; a separate left/right marker is not always retained.
- Derived heart rate is an approximation from available set maxima, not a continuously measured sensor trace.
- Ski timing may differ from the source; stroke counts are not currently exported.
- Speediance or Garmin service changes can affect sign-in and transfers. Automated tests do not replace Android device, update or live-account testing. The code-2001 handling has been tested with simulated responses; it does not guarantee that every server-side failure is resolved.

## About this repository

This repository distributes APKs and public release information and collects beta feedback. Source code is maintained privately. The maintainer publishes APKs manually.

Speed2GC is independent and is not affiliated with or endorsed by Garmin or Speediance. Product names and trademarks belong to their respective owners.
