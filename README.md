# iRanger

**Offline-first field tool for wildlife rangers and conservation volunteers.**

Log incidents, track observations, and manage team assignments — all from a single HTML file with no server, no account, and no internet required. Data stays in your browser.

---

## Features

- **Incident ticketing** — Jira-style workflow: Open → Assigned → In Progress → Escalated → Resolved
- **Field observations** — GPS-tagged notes for species sightings, tracks, nests, water issues, and more
- **My Cases** — personal view of every ticket you reported or were assigned
- **Team management** — role-based access for Rangers, Coordinators, and Supervisors
- **PIN login** — each team member selects their account and authenticates with a 4-digit PIN
- **User admin** — Supervisors can add, edit, and remove user accounts in-app
- **Offline-first** — works with no internet connection; data never leaves the device
- **Export** — download incidents or observations as CSV, full backup as JSON, or print a formatted PDF report
- **Responsive** — desktop sidebar layout and mobile bottom-nav, same file

---

## Getting Started

No installation. No build step.

1. Download `iranger.html`
2. Open it in any modern browser
3. On first launch, create a Supervisor account with your name and a 4-digit PIN
4. Go to **Profile → Manage Accounts** to add your team

That's it.

To share with your team, send them the same HTML file. Each person creates their own account on first use, or a Supervisor adds them in advance.

---

## User Roles

| Role | Can do |
|---|---|
| **Ranger** | Log incidents and observations, update status of own cases |
| **Coordinator** | Everything above + assign incidents to team members, view all cases |
| **Supervisor** | Everything above + escalation resolution, user account management |

The first account created is always a Supervisor. Additional roles are assigned by a Supervisor via **Profile → Manage Accounts**.

---

## Incident Workflow

```
[Ranger logs incident]
        ↓
      Open
        ↓
   Assigned        ← Coordinator assigns to a team member
        ↓
  In Progress      ← Assigned ranger starts work
        ↓
   Escalated       ← Flagged to Supervisor if needed
        ↓
    Resolved       ← Supervisor or Coordinator closes with notes
```

Every status change is logged with the user's name, timestamp, and optional notes — a full audit trail per incident.

---

## Exporting Data

From **Profile → Export Data**:

| Format | Contents |
|---|---|
| **JSON** | Full backup — all incidents, observations, users (no PINs) |
| **Incidents CSV** | Title, type, severity, status, GPS, reporter, assignee, timestamps |
| **Observations CSV** | Type, notes, GPS, reporter, date |
| **Print Report** | Formatted incident table — save as PDF via browser print dialog |

---

## Data & Privacy

- All data is stored in the browser's `localStorage`
- Nothing is sent to any server
- PINs are stored locally and never included in exports
- Clearing browser data or localStorage will erase all records — use the JSON export regularly as a backup
- To move data between devices, export JSON and manually import by pasting into browser console: `localStorage.setItem('ir_incidents', JSON.stringify([...]))`

---

## Technical Details

- **Single file** — one `.html` file, no build tooling, no dependencies to install
- **Storage** — browser `localStorage` (~5–10 MB limit depending on browser)
- **Map** — [Leaflet](https://leafletjs.com/) loaded from CDN (requires internet on first load for map tiles)
- **GPS** — uses browser `navigator.geolocation` API; requires HTTPS or `localhost` in some browsers
- **Photos** — captured via device camera or file picker, stored as base64 in localStorage; keep photos small to stay within storage limits
- **Languages** — English default, Hungarian (`HU`) toggle available

---

## Roadmap

- [ ] Backend sync (Supabase / Firebase) for real-time team sharing
- [ ] Push notifications for escalated incidents
- [ ] Species reference library (offline)
- [ ] Map view with incident pins per patrol area
- [ ] Import JSON to restore or merge datasets
- [ ] PWA manifest for "Add to Home Screen" on mobile

---

## Contributing

Pull requests are welcome. For major changes, open an issue first.

The entire application lives in `iranger.html`. Key sections are clearly marked with `═══` comments:

```
// ═══════════════ CONSTANTS ═══════════════
// ═══════════════ DB ═══════════════
// ═══════════════ STATE ═══════════════
// ═══════════════ LOGIN ═══════════════
// ═══════════════ MAIN RENDER ═══════════════
// ═══════════════ INCIDENTS ═══════════════
// ═══════════════ OBSERVATIONS ═══════════════
// ═══════════════ DASHBOARD ═══════════════
// ═══════════════ PROFILE ═══════════════
// ═══════════════ USER ADMIN ═══════════════
// ═══════════════ INIT ═══════════════
```

To add a new language, copy the `en` block inside the `TR` object and translate the values.

---

## License

[MIT](LICENSE)
