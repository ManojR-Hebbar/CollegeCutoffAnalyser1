# Colleges map / links feature — status

## Done
- **College-links dialog** (`CutoffResultAdapter.showCollegeLinksDialog`, `dialog_college_links.xml`)
  — tapping a college name opens a dialog with a caution note plus a "Website" and/or "Map
  Location" button, whichever links exist for that college in `common.db`. Shipped, live for all
  users.
- **Firebase Analytics**: `college_links_dialog_opened` event added (`AnalyticsHelper.java`),
  logged every time the dialog opens, with `college_code`, `has_website`, `has_map` params.
- **Colleges map screen** (`CollegesMapActivity`) — code-complete, pins colleges with code-labeled
  markers, wired to the `fabMap` FAB on `ResultsActivity`. Verified crash-free on an emulator.
- `lat`/`lng` columns added to the `colleges` table in `common.db`, populated from COMEDK's
  embed-map data (163/249 colleges covered, no API key needed for those).
- Geocoding script for the remaining KEA-only colleges written
  (`dataLab/Step0.0_ExamType/Common/geocode_kea_only.py`), not yet run (needs the API key below).

## Not done / blocked
- **Map FAB hidden** (`activity_results.xml` — `fabMap` set to `android:visibility="gone"`) until
  the map feature is verified end-to-end with real pins. The click listener in
  `ResultsActivity.java` is untouched, so re-enabling is a one-line visibility flip.
- **Blocked on a Google Maps API key**, which only the account owner can provision:
  1. In GCP project `college-cutoff-analyser`, enable **Maps SDK for Android** + **Geocoding API**,
     confirm billing is linked (required by Maps Platform even within the free tier).
  2. Restrict the key in `app/google-services.json` (or a new dedicated key) to those two APIs +
     the app's package name/SHA-1 fingerprints.
  3. Put the key in `local.properties` as `MAPS_API_KEY=...` (gitignored, read via
     `app/build.gradle.kts` → `manifestPlaceholders["mapsApiKey"]`).
  4. Run `GOOGLE_MAPS_API_KEY=<key> python dataLab/Step0.0_ExamType/Common/geocode_kea_only.py` to
     geocode the ~83 KEA-only colleges still missing coordinates.
- Once the key is in place: rebuild `common.db` → re-run `encrypt_common_db.py` → bump
  `AppDatabase.DATA_VERSION` (currently 4, next ship is 5) → rebuild app → verify pins actually
  render on a real device/emulator (a missing/invalid key silently shows a blank grey map with just
  the Google wordmark — no error — so "it opened" is not sufficient proof) → flip `fabMap`'s
  visibility back to `visible`.
