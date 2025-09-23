# Calendar Prompt Injector (Google Apps Script)
Turn any recurring Google Calendar event into a daily **smart prompt** generator.

- Injects a fresh prompt into the event **description** at a scheduled time (default: **12:45 PM** in your time zone).
- Works with **one or many events** (e.g., `thinking walk`, `deep work 1`).
- Runs fully in your Google account via **Google Apps Script** - no servers.

## Quick start (2–3 min)
1. Go to **https://script.google.com** → **New project**.
2. In the editor: **Services → + → Calendar API** (enable the *Advanced* one).
3. Copy the contents of `src/Code.gs` and `src/Prompts.gs` into your project.
4. In `Code.gs`, set your calendar ID and events in `CONFIG` (or use defaults).
5. Run **`installTriggers()`** and approve permissions.
6. Optionally run **`updateToday()`** once to test.

## Features
- **Multiple events** supported via `CONFIG.EVENTS` (each with its own time window & prompt bank).
- **Deterministic random**: every day picks a stable prompt (won’t change if the script re-runs).
- **Idempotent**: won’t duplicate the same day’s header.
- **Conflict-safe option**: (disabled by default) auto-reschedule if the event is booked; see `AUTO_MOVE` in CONFIG.

## Customize
- Edit **`src/Prompts.gs`** to change prompt banks or add your own (e.g., `security`, `tooling`, `research`).
- Point an event at a specific bank with `bank: 'security'`.
- Change time / timezone in `CONFIG`.

## Example: single event
```js
const CONFIG = {
  TZ: 'America/Los_Angeles',
  CAL_ID: 'primary',
  TRIGGER_HOUR: 12,
  TRIGGER_MINUTE: 45,
  AUTO_MOVE: false, // if true, will try to move a conflicted instance
  EVENTS: [
    { title: 'thinking walk', start: {h:13,m:0}, end: {h:13,m:45}, bank: 'default' },
  ],
};
```

## Example: two events
```js
EVENTS: [
  { title: 'thinking walk', start: {h:13,m:0},  end: {h:13,m:45}, bank: 'default' },
  { title: 'deep work 1',   start: {h:7,m:0},   end: {h:8,m:45},  bank: 'research' },
],
```

## License
MIT © Krti Tallam
