# 🛏️ Smart Design Bed Shop — Management System

A clean, modern business management system built for bed retailers. Manage your inventory, customers, sales, expenses, and reports from one professional dashboard.

---

## ✨ Features

| Section | What you can do |
|---|---|
| **Dashboard** | Live overview — today's sales, monthly totals, inventory value, outstanding balances, low-stock alerts |
| **Inventory** | Add, edit, delete products · Track stock levels · Low-stock warnings |
| **Customers** | Customer records · Outstanding account balances · Search |
| **Sales** | Record sales (Cash / Card / Account) · Auto-deducts stock · Updates customer balances |
| **Expenses** | Log Rent, Electricity, Fuel, Salaries, Repairs, General costs |
| **Reports** | Revenue · Cost of Goods · Gross Profit · Net Profit · Payment method breakdown · Outstanding accounts |
| **Settings** | Business name, phone, email, address, VAT number |

**Design:** Royal Blue & Navy sidebar · Gold accents · Color-coded badges · Fully responsive (desktop, tablet, mobile)

---

## 🚀 Quick Start (Local Development)

### Prerequisites
- [Node.js](https://nodejs.org/) version **18 or higher**
- npm (comes with Node.js)

### Steps

```bash
# 1. Clone the repository
git clone https://github.com/YOUR_USERNAME/smart-design-bed-shop.git

# 2. Enter the project folder
cd smart-design-bed-shop

# 3. Install dependencies
npm install

# 4. Start the development server
npm run dev
```

Then open **http://localhost:5173** in your browser.

---

## 📁 Project Structure

```
smart-design-bed-shop/
├── public/
│   └── favicon.svg          # App icon
├── src/
│   ├── main.jsx             # React entry point
│   └── App.jsx              # Full application (all pages & logic)
├── index.html               # HTML shell
├── package.json             # Dependencies & scripts
├── vite.config.js           # Vite configuration
├── vercel.json              # Vercel deployment config
├── .gitignore
└── README.md
```

---

## ☁️ Deploy to Vercel (Free Hosting)

### Option 1 — Vercel Dashboard (Recommended, easiest)

1. Push your code to GitHub (see below)
2. Go to [vercel.com](https://vercel.com) and sign in with GitHub
3. Click **"Add New Project"**
4. Select your **smart-design-bed-shop** repository
5. Vercel auto-detects Vite — click **"Deploy"**
6. Your app is live in ~60 seconds ✅

### Option 2 — Vercel CLI

```bash
# Install Vercel CLI
npm install -g vercel

# Deploy from the project folder
vercel

# Follow the prompts — it auto-detects Vite settings
```

---

## 🐙 Push to GitHub

If you haven't set up Git yet:

```bash
# Inside your project folder:
git init
git add .
git commit -m "Initial commit — Smart Design Bed Shop"

# Create a new repo on github.com, then:
git remote add origin https://github.com/YOUR_USERNAME/smart-design-bed-shop.git
git branch -M main
git push -u origin main
```

---

## 🛠️ Build for Production

```bash
npm run build
```

This creates a `dist/` folder with optimised files ready for any static host.

To preview the production build locally:

```bash
npm run preview
```

---

## 📱 Responsive Design

The app works on all screen sizes:

- **Desktop / Laptop** — Full sidebar + wide table layout
- **Tablet** — Sidebar collapses, content adjusts
- **Mobile Phone** — Hamburger menu, stacked cards, scrollable tables

---

## 🔧 Customisation

All data and seed records are in `src/App.jsx`. To change the demo data, edit the arrays at the top of the file:

```js
// Change these to your own products:
const SEED_PRODUCTS = [ ... ]

// Change these to your own customers:
const SEED_CUSTOMERS = [ ... ]
```

To change the shop name shown in the sidebar, update the `Settings` component or the brand section in the sidebar.

---

## 🧱 Tech Stack

| Tool | Purpose |
|---|---|
| [React 18](https://react.dev/) | UI framework |
| [Vite 5](https://vitejs.dev/) | Build tool & dev server |
| Inline styles + CSS | Styling (no external CSS library needed) |

No database required — data lives in React state (in-memory). To persist data across sessions, the app can be extended with localStorage or a backend API.

---

## 📄 License

MIT — free to use, modify, and deploy for your own business.

---

## 🙏 Credits

Built for **Smart Design Bed Shop** · Durban, South Africa

