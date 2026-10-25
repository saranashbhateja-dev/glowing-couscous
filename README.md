# JEE OS 3.2.0 — Fixed Daily Lecture Plan + Cloud Sync

JEE OS 3.0 is rebuilt around the chapter names, lecture counts and coaching links in the supplied `Brave.txt` file.

## Curriculum loaded
- Physics: 32 chapter entries / 325 listed lectures
- Chemistry: 38 chapter entries / 333 listed lectures (updated from the latest supplied Brave.txt)
- Mathematics: 34 chapter entries / 298 listed lectures
- Total: 104 chapter entries / 956 listed lectures

Chapter order and repeated titles are preserved exactly as supplied. Each chapter's Watch link uses the supplied URL when its title/count/link mapping is clear.

## Daily execution
On study days, the planner schedules up to six lectures in this fixed order:
1. Physics — two lectures
2. Chemistry — two lectures
3. Mathematics — two lectures

Each subject progresses independently through its own chapter list. The planner is lecture-count based, not duration based. Sunday remains protected for the existing test/rest system.

### Daily DPP and practice checklist
- One persistent DPP checkbox for each scheduled lecture (normally six DPPs per study day).
- One separate daily practice checkbox for Physics, Chemistry and Mathematics (three practice tasks per calendar day).
- DPP completion is tied to the lecture, so it remains checked if that lecture appears again after being carried forward.
- Practice completion is date-specific and resets naturally on the next calendar date.

## Revision and tests
The existing six-cycle chapter revision schedule and Sunday test framework are retained. A chapter's revision cycle begins when all its counted lectures are marked complete. The test system continues to use planned chapter completion dates and logged test results.

## Data quality note
The latest `Brave(1).txt` resolves the earlier Chemistry row issue: Chemical Kinetics has 13 lectures and its link, while the second P-Block Elements entry has 6 lectures and its matching Inorganic Chemistry link. Both entries remain distinct and in their supplied order.

## Run on Windows
1. Install Node.js 22 or newer.
2. Extract this ZIP to a writable folder.
3. Double-click `start.bat`.
4. The app opens at `http://127.0.0.1:3000`.
Do not open `index.html` directly.

## Supabase cloud sync (web + Android)
- Uses the existing Supabase project configured in `app.js`; sign in with the same account on desktop and Android.
- Local-first: each change is saved to local storage immediately and queued for cloud sync.
- `jeeo_cloud_state` stores one per-user JSON snapshot, with RLS restricting rows to `auth.uid()`; the client uses only the publishable key.
- Snapshot saves are atomic and include lecture progress, chapter state, revisions, tests, DPP checkboxes, daily practice, plan settings and manual chapter order.
- Realtime updates refresh other signed-in devices when a newer snapshot arrives; app resume/online events also pull the latest snapshot.
- Legacy users without a snapshot are loaded from the existing `jeeo_*` tables and then seeded into the snapshot without deleting those legacy rows.
- Offline changes remain local and are marked as pending for that signed-in account; when connectivity returns, the app pushes pending changes before pulling remote state. The status pill shows local, saving, saved or failed state.
- Last-write-wins applies if two devices edit the same account simultaneously while offline. Open the app online on both devices to minimize conflicts.

## Data and backups
- Progress is saved in browser-local storage.
- Use Settings → Download backup to export progress.
- This build uses a new local storage key so it does not silently mix the old 2.5.x curriculum/progress with this new curriculum.
- Optional Supabase sync configuration is retained from the previous project. If you previously used cloud sync with the old OS, do not sign in until the new curriculum migration has been reviewed; old cloud module rows may still exist.

## Android
Capacitor configuration and the GitHub Actions debug APK workflow are retained. The APK is not prebuilt in this ZIP.


UI refresh 3.2.0: premium responsive dark interface, motion refinements, and dashboard blank-screen fix. See `UI-REFRESH-3.2.0.txt`.
