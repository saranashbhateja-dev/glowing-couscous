# JEE OS 3.0.0 — Build Audit

## Source mapping
- Parsed the supplied `Brave.txt` chapter list in source order.
- Physics: 32 entries, 325 lecture counts.
- Chemistry: 38 entries, 327 known lecture counts; row 23 has a missing count and mismatched URL slug and remains explicitly unresolved.
- Mathematics: 34 entries, 298 lecture counts.
- Repeated or similarly named chapter entries were retained as separate records.

## Implemented
- Replaced the previous curriculum seed with the supplied chapter names, lecture counts, and coaching URLs.
- Changed daily scheduling from duration-based packing to a fixed per-subject target: up to two Physics lectures, then two Chemistry lectures, then two Mathematics lectures.
- Added persistent DPP completion per lecture and date-specific daily practice checkboxes for each subject.
- Preserved existing revision cycles, Sunday test planning, test result logging, calendar, chapter progress, backup/import, and Android build workflow.
- Changed the local storage key to isolate this new curriculum from previous 2.5.x browser state.
- Removed the obsolete duration refresh script/cache dependency from the user-facing workflow.

## Validation
- `node --check app.js` is run as part of the packaging process.
- JSON syntax and curriculum counts are validated by the build script.
- Browser interaction, Supabase cloud migration, and Android runtime have not been end-to-end tested in this environment.

## Known issue requiring user confirmation
Chemistry source row 23 is titled `P-Block Elements`, has no lecture count, and points to a URL whose slug is `chemical-kinetics`. The supplied URL is retained as `sourceUrl` but not made clickable. No count or corrected title has been invented.
