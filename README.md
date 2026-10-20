# VedraInvoice Phase 2 — Cloud App

React + Vite + Supabase authentication/database app for invoicing. Includes cloud-saved customers, products, invoices, business settings, RLS policies, PDF invoice downloads, CSV export, partial/full payment recording, UPI QR generation, JSON backup/restore, reports, and responsive UI.

> Important: source code is provided, but it cannot be connected to your Supabase project or deployed under your accounts automatically. Complete the setup steps below. This is a starter production architecture, not a certified GST filing product; validate before using it for real financial records.

## 1. Create Supabase backend
1. Create a project at https://supabase.com/ and save the database password privately.
2. Open **SQL Editor** in the project dashboard.
3. Paste and run the full `supabase/schema.sql` file.
4. In **Project Settings → API** (or Connect), copy the Project URL and the publishable key / anon public key. Never use a `service_role` key in this browser app.
5. Under **Authentication → URL Configuration**, set your local Site URL to `http://localhost:5173`. Add your deployed URL to Redirect URLs after deployment.
6. For easy initial testing, Supabase email confirmation can remain enabled; signup will ask the user to verify email before signing in. Configure SMTP before a public launch if reliable email delivery is required.

## 2. Configure and run
Requires Node.js 18+.

```bash
cp .env.example .env
# edit .env and set the real Supabase project URL and publishable/anon key
npm install
npm run dev
```

Windows: copy `.env.example` to `.env` using File Explorer or `copy .env.example .env` in Command Prompt. Put the same two environment variables into `.env`.

## 3. Deploy and get a public URL
### Netlify
1. Push the project folder to a GitHub repository.
2. Import the repository in Netlify.
3. Build command: `npm run build`; publish directory: `dist`.
4. Add `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` under Site configuration → Environment variables.
5. Deploy the site, then add the resulting URL to Supabase Authentication → URL Configuration → Redirect URLs and set Site URL as appropriate.

### Vercel
Import the repository into Vercel, set framework Vite, build command `npm run build`, output directory `dist`, and add the same two environment variables. Deploy and configure the URL in Supabase Auth.

Do not commit `.env` or share private database credentials. The public/anon key is designed to be used by the frontend only when Row Level Security is correctly enabled; never expose a service-role key.

## Features
- Email/password sign up and sign in via Supabase Auth
- Row Level Security on all user-owned tables
- Cloud CRUD for customers, products, invoices and business settings
- GST line-item calculation with intra-state CGST+SGST or inter-state IGST display
- PDF invoice download
- UPI payment QR generation (requires a UPI ID in Settings; QR only initiates payment, it does not verify/collect money)
- Partial and full payment recording
- CSV invoice export; JSON backup and restore
- Dashboard, reports, search, dark mode, mobile layout

## Known limitations / production checklist
- This code does not integrate a payment gateway, verify UPI receipts, send invoices by email, support team/role management, or file GST returns.
- Invoice items are stored as JSONB. Customer/product/invoice operations are protected with RLS, but you should run a security review and test cross-account access before launch.
- PDF format and tax treatment must be reviewed by an accountant for your business, transaction type, place of supply, HSN/SAC and current GST rules.
- Configure custom SMTP, rate limits, backups, monitoring, a privacy policy, terms, and secure account recovery before public SaaS launch.
- Supabase free-tier limits and hosting provider terms/pricing may change. Public availability depends on your own deployment account and configuration.
