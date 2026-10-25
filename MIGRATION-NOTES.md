# Jee OS rebuild

- Input: uploaded `Jee Tracker.zip` only.
- `tracker.json` preserved as exact source seed.
- `curriculum.json` derived only from that source.
- Original UI/planner/revision/test logic preserved.
- State backend separated into Supabase `jeeo_*` tables.
- Node server is static-only.
- Dark mode only.
- Port 3000.

JEE OS 3.0.0 uses a fresh local-storage key and a new lecture-count-based curriculum. Review the Chemistry row 23 warning in README.md before treating that entry as complete.
