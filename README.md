# Sugar Operations Dashboard

A mobile-first truck loading operations dashboard for managing daily warehouse appointments, driver coordination, and client accountability.

**Live:** [lokio23.github.io/sugar-operations-dashboard](https://lokio23.github.io/sugar-operations-dashboard/)

---

## What It Does

Manages 50+ daily truck loads across multiple time slots and warehouse bays. Tracks which trucks have loaded, which missed their slot, and keeps clients accountable for fines.

- **Daily Board** — Real-time view of loaded, missed, and remaining trucks for any day
- **Schedule** — 30-day forward booking with bulk truck creation
- **Overview** — Per-client progress tracking (Rocky & Marco), total stats, and fine calculations
- **Truck Details** — Edit appointment codes, drivers, truck numbers, phone, carrier, and notes
- **Bay Capacity** — Configurable bays per time slot with overbooking prevention

## Tech Stack

| Layer | Tech |
|-------|------|
| Frontend | Single HTML file with inline CSS & vanilla JS |
| Backend | [Supabase](https://supabase.com) (PostgreSQL + Auth RPC) |
| Hosting | GitHub Pages (auto-deploys on push to main) |
| Design | Mobile-first, iOS home screen app compatible |

No build step. No dependencies to install. Just one file.

## Getting Started

### Run Locally

```bash
git clone https://github.com/lokio23/sugar-operations-dashboard.git
cd sugar-operations-dashboard
npx http-server . -c-1
```

Open `http://localhost:8080` and log in with a team PIN.

### Add to iPhone Home Screen

1. Open the live URL in Safari
2. Tap Share → Add to Home Screen
3. "Makes Sense Supply" appears as a standalone app
4. Pull down to refresh data

## Database

Powered by Supabase with three tables:

| Table | Purpose |
|-------|---------|
| `trucks` | All truck records (buyer, date, time slot, code, driver, status, etc.) |
| `team_members` | Team login credentials with RLS-protected PINs |
| `login_attempts` | Rate limiting (10 attempts/min) |

## Configuration

The `CONFIG` object in `index.html` controls:

- **Bays per slot** — Max trucks per time slot (also editable in the Overview tab UI)
- **Time slots** — The day's appointment windows
- **Buyer targets** — Per-client truck goals and colors
- **Fine per miss** — Dollar amount per missed truck (editable in UI)

## Security

- PIN-based auth via Supabase RPC (PINs never exposed to frontend)
- Row Level Security on all tables
- XSS escaping on all user inputs
- 12-hour sessions stored in sessionStorage
- Supabase anon key is frontend-safe by design; sensitive operations protected by RLS

## Roadmap

- [ ] Driver roster with contact management
- [ ] Bulk appointment code import
- [ ] SMS/email notifications to drivers (Twilio + Resend)
- [ ] Client portal (read-only, filtered by buyer)
- [ ] Driver mobile view for self-service
- [ ] Auto-flag overdue trucks with quick-action buttons

---

Built by [Makes Sense Supply](https://github.com/lokio23)
