# Royal Bed Shop — Management System

Premium, responsive bed shop management app for phone, tablet, and desktop.
Built with **TanStack Start (React 19) + Vite 7 + Tailwind CSS v4 + shadcn/ui**.
No login required — all data is stored locally in the browser for instant demo.

> Royal Blue + Gold premium UI · rounded cards · gradients · soft shadows · responsive layout.

---

## Features

- 📊 **Dashboard** – today / weekly / monthly sales, orders waiting, deliveries, low stock, customers, outstanding payments, inventory value, recent activity, quick actions
- 📦 **Inventory** – add / edit / archive / delete products (name, code, category, brand, size, supplier, cost, price, qty, reorder, description)
- 👤 **Customers** – profiles, balances, history
- 🚚 **Suppliers** – contacts and outstanding payments
- 🛒 **Sales & Invoices** – quick sales, cash / card / EFT, VAT, save, print
- 📋 **Orders & Deliveries** – auto-created from sales, status workflow (pending → processing → ready → delivered)
- ↩️ **Returns** – restock and mark invoice as returned
- 💰 **Expenses** – rent, electricity, salaries, fuel, advertising, repairs, supplier payments
- 📈 **Reports** – 14-day sales chart, expenses by category, best sellers, low-stock alerts, estimated profit
- ⚙️ **Settings** – business info, VAT %, numbering prefixes, currency, reset demo data

---

## Tech Stack

- React 19 + TanStack Start v1 (SSR-ready, file-based routing)
- Vite 7 (build) · TypeScript (strict)
- Tailwind CSS v4 + shadcn/ui components
- Recharts (charts) · Lucide (icons) · Sonner (toasts)
- LocalStorage persistence (zero-backend demo)

---

## Run Locally

```bash
# install
bun install        # or: npm install / pnpm install

# dev
bun dev            # http://localhost:8080

# production build
bun run build
bun run preview
```

---

## Deploy to Vercel

This repo is ready for Vercel out of the box.

### One-click

1. Push the repo to GitHub.
2. On https://vercel.com → **New Project** → import your repo.
3. Vercel auto-detects Vite. Confirm:
   - **Build command:** `npm run build`
   - **Output directory:** `dist`
4. Click **Deploy**.

The included `vercel.json` rewrites all client routes to `index.html`
so deep links like `/inventory` and `/sales` work on refresh.

### CLI

```bash
npm i -g vercel
vercel        # follow prompts
vercel --prod # deploy production
```

---

## Push to GitHub

```bash
git init
git add .
git commit -m "Initial commit: Royal Bed Shop"
git branch -M main
git remote add origin https://github.com/<your-username>/royal-bed-shop.git
git push -u origin main
```

---

## Project Structure

```
src/
  components/        # AppShell, StatCard, shadcn/ui
  lib/store.ts       # LocalStorage-backed data store
  routes/
    __root.tsx       # Root layout + meta + toaster
    _app.tsx         # Sidebar shell layout (pathless)
    _app.index.tsx   # /            – Dashboard
    _app.inventory.tsx
    _app.customers.tsx
    _app.suppliers.tsx
    _app.sales.tsx
    _app.orders.tsx
    _app.returns.tsx
    _app.expenses.tsx
    _app.reports.tsx
    _app.settings.tsx
  styles.css         # Design tokens (Royal Blue / Gold theme)
```

---

## Data

The demo seeds 4 products, 2 customers, 2 suppliers, and 2 expenses on first run.
Use **Settings → Reset demo data** to restore defaults.

To wire up a real backend later, replace `src/lib/store.ts` with API calls
(e.g., Lovable Cloud / Supabase). The UI consumes a typed `DB` interface,
so swapping the data layer is contained to one file.

---

## License

MIT
