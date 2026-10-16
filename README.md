# Peter's Work Manager

Private, single-user work logging and invoicing starter application.

## Run locally

1. Install Node.js 20+.
2. `npm install`
3. Copy `.env.example` to `.env` and configure `SESSION_SECRET`, `ADMIN_PASSWORD`, business details and SMTP credentials.
4. `npm start` and open `http://localhost:3000`.

## Hosting

GitHub hosts the source code, **not** this Node.js application. Deploy to a Node.js host with persistent disk and HTTPS. Back up `workmanager.sqlite` regularly. Configure `NODE_ENV=production`, HTTPS reverse proxy and a production session store before public use. Never commit `.env` or the SQLite database.

## Automated billing

Set `CRON_SECRET` and configure a scheduler to POST daily to `/tasks/billing` with `Authorization: Bearer YOUR_CRON_SECRET`. It invoices only unbilled jobs at the end of each client's selected billing period, and attempts SMTP delivery. Missing SMTP settings mean no automatic delivery. Review accounting and VAT requirements before issuing real invoices.

## Limitations

This is a functional MVP, not a production-hardened accounting platform. It does not yet support overnight shifts, rate history, credit notes, VAT, tax compliance validation, CSRF protection, persistent sessions, or automated backup. Changes to a client's rate can affect the calculation for previously unbilled work. Test with dummy clients first.

## Mobile work-entry update
- The work-entry page is responsive for small mobile screens, with large touch controls.
- The date field defaults to **today in the phone's local timezone**, and any other date can be selected.
- Multiple sessions can be logged on the same day, for the same or different clients, with independent start/end times.
- The selected day's sessions and total hours/earnings are shown below the form.
- Existing jobs and invoice records are preserved when updating the application files.
