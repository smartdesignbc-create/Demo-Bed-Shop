import { useState, useEffect } from "react";

// ─── Seed Data ──────────────────────────────────────────────────────────────
const SEED_PRODUCTS = [
  { id: 1, name: "Luxury King Bed Frame", category: "Beds", cost: 3200, price: 5800, stock: 8, sku: "BED-K001" },
  { id: 2, name: "Queen Divan Base", category: "Beds", cost: 1800, price: 3200, stock: 12, sku: "BED-Q002" },
  { id: 3, name: "Single Mattress (Foam)", category: "Mattresses", cost: 600, price: 1100, stock: 20, sku: "MAT-S003" },
  { id: 4, name: "Orthopedic Queen Mattress", category: "Mattresses", cost: 2400, price: 4200, stock: 6, sku: "MAT-Q004" },
  { id: 5, name: "Headboard – Velvet Navy", category: "Headboards", cost: 900, price: 1600, stock: 4, sku: "HEAD-005" },
  { id: 6, name: "Bed Linen Set (King)", category: "Accessories", cost: 350, price: 680, stock: 30, sku: "ACC-006" },
];

const SEED_CUSTOMERS = [
  { id: 1, name: "Thandi Nkosi", phone: "071 234 5678", email: "thandi@email.com", balance: 2400, address: "12 Oak St, Durban" },
  { id: 2, name: "Rajesh Pillay", phone: "082 987 6543", email: "rajesh@email.com", balance: 0, address: "45 Lotus Rd, Phoenix" },
  { id: 3, name: "Sarah van der Berg", phone: "060 111 2233", email: "sarah@email.com", balance: 5800, address: "88 Palm Ave, Hillcrest" },
];

const SEED_SALES = [
  { id: 1, date: "2025-06-28", customer: "Thandi Nkosi", product: "Luxury King Bed Frame", qty: 1, total: 5800, paid: 3400, method: "Account" },
  { id: 2, date: "2025-06-28", customer: "Walk-in", product: "Single Mattress (Foam)", qty: 2, total: 2200, paid: 2200, method: "Cash" },
  { id: 3, date: "2025-06-27", customer: "Rajesh Pillay", product: "Orthopedic Queen Mattress", qty: 1, total: 4200, paid: 4200, method: "Card" },
  { id: 4, date: "2025-06-26", customer: "Sarah van der Berg", product: "Headboard – Velvet Navy", qty: 2, total: 3200, paid: 0, method: "Account" },
];

const SEED_EXPENSES = [
  { id: 1, date: "2025-06-01", category: "Rent", description: "June shop rent", amount: 8500 },
  { id: 2, date: "2025-06-05", category: "Electricity", description: "Municipal account", amount: 1200 },
  { id: 3, date: "2025-06-10", category: "Fuel", description: "Delivery vehicle", amount: 640 },
];

// ─── Helpers ─────────────────────────────────────────────────────────────────
const fmt = (n) => `R ${Number(n).toLocaleString("en-ZA", { minimumFractionDigits: 2 })}`;
const today = () => new Date().toISOString().slice(0, 10);

// ─── Icons (inline SVG) ──────────────────────────────────────────────────────
const Icon = ({ name, size = 20 }) => {
  const icons = {
    dashboard: <path d="M3 13h8V3H3v10zm0 8h8v-6H3v6zm10 0h8V11h-8v10zm0-18v6h8V3h-8z"/>,
    inventory: <path d="M20 6h-2.18c.07-.44.18-.87.18-1.33C18 2.54 16.46 1 14.55 1c-1.23 0-2.3.64-3 1.67L11 4.14l-.55-1.47C9.7 1.64 8.63 1 7.45 1 5.54 1 4 2.54 4 4.67c0 .46.1.89.18 1.33H2C.9 6 0 6.9 0 8v12c0 1.1.9 2 2 2h18c1.1 0 2-.9 2-2V8c0-1.1-.9-2-2-2z"/>,
    customers: <path d="M16 11c1.66 0 2.99-1.34 2.99-3S17.66 5 16 5c-1.66 0-3 1.34-3 3s1.34 3 3 3zm-8 0c1.66 0 2.99-1.34 2.99-3S9.66 5 8 5C6.34 5 5 6.34 5 8s1.34 3 3 3zm0 2c-2.33 0-7 1.17-7 3.5V19h14v-2.5c0-2.33-4.67-3.5-7-3.5zm8 0c-.29 0-.62.02-.97.05 1.16.84 1.97 1.97 1.97 3.45V19h6v-2.5c0-2.33-4.67-3.5-7-3.5z"/>,
    sales: <path d="M7 18c-1.1 0-1.99.9-1.99 2S5.9 22 7 22s2-.9 2-2-.9-2-2-2zM1 2v2h2l3.6 7.59-1.35 2.45c-.16.28-.25.61-.25.96C5 16.1 6.9 18 9 18h12v-2H9.42c-.14 0-.25-.11-.25-.25l.03-.12.9-1.63H19c.75 0 1.41-.41 1.75-1.03l3.58-6.49c.08-.14.12-.31.12-.48 0-.55-.45-1-1-1H5.21l-.94-2H1zm16 16c-1.1 0-1.99.9-1.99 2s.89 2 1.99 2 2-.9 2-2-.9-2-2-2z"/>,
    orders: <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zm-7 3c1.93 0 3.5 1.57 3.5 3.5S13.93 13 12 13s-3.5-1.57-3.5-3.5S10.07 6 12 6zm7 13H5v-.23c0-.62.28-1.2.76-1.58C7.47 15.82 9.64 15 12 15s4.53.82 6.24 2.19c.48.38.76.97.76 1.58V19z"/>,
    expenses: <path d="M11.8 10.9c-2.27-.59-3-1.2-3-2.15 0-1.09 1.01-1.85 2.7-1.85 1.78 0 2.44.85 2.5 2.1h2.21c-.07-1.72-1.12-3.3-3.21-3.81V3h-3v2.16c-1.94.42-3.5 1.68-3.5 3.61 0 2.31 1.91 3.46 4.7 4.13 2.5.6 3 1.48 3 2.41 0 .69-.49 1.79-2.7 1.79-2.06 0-2.87-.92-2.98-2.1h-2.2c.12 2.19 1.76 3.42 3.68 3.83V21h3v-2.15c1.95-.37 3.5-1.5 3.5-3.55 0-2.84-2.43-3.81-4.7-4.4z"/>,
    reports: <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>,
    settings: <path d="M19.14 12.94c.04-.3.06-.61.06-.94 0-.32-.02-.64-.07-.94l2.03-1.58c.18-.14.23-.41.12-.61l-1.92-3.32c-.12-.22-.37-.29-.59-.22l-2.39.96c-.5-.38-1.03-.7-1.62-.94l-.36-2.54c-.04-.24-.24-.41-.48-.41h-3.84c-.24 0-.43.17-.47.41l-.36 2.54c-.59.24-1.13.57-1.62.94l-2.39-.96c-.22-.08-.47 0-.59.22L2.74 8.87c-.12.21-.08.47.12.61l2.03 1.58c-.05.3-.09.63-.09.94s.02.64.07.94l-2.03 1.58c-.18.14-.23.41-.12.61l1.92 3.32c.12.22.37.29.59.22l2.39-.96c.5.38 1.03.7 1.62.94l.36 2.54c.05.24.24.41.48.41h3.84c.24 0 .44-.17.47-.41l.36-2.54c.59-.24 1.13-.56 1.62-.94l2.39.96c.22.08.47 0 .59-.22l1.92-3.32c.12-.22.07-.47-.12-.61l-2.01-1.58zM12 15.6c-1.98 0-3.6-1.62-3.6-3.6s1.62-3.6 3.6-3.6 3.6 1.62 3.6 3.6-1.62 3.6-3.6 3.6z"/>,
    plus: <path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z"/>,
    edit: <path d="M3 17.25V21h3.75L17.81 9.94l-3.75-3.75L3 17.25zM20.71 7.04c.39-.39.39-1.02 0-1.41l-2.34-2.34c-.39-.39-1.02-.39-1.41 0l-1.83 1.83 3.75 3.75 1.83-1.83z"/>,
    trash: <path d="M6 19c0 1.1.9 2 2 2h8c1.1 0 2-.9 2-2V7H6v12zM19 4h-3.5l-1-1h-5l-1 1H5v2h14V4z"/>,
    close: <path d="M19 6.41L17.59 5 12 10.59 6.41 5 5 6.41 10.59 12 5 17.59 6.41 19 12 13.41 17.59 19 19 17.59 13.41 12z"/>,
    search: <path d="M15.5 14h-.79l-.28-.27C15.41 12.59 16 11.11 16 9.5 16 5.91 13.09 3 9.5 3S3 5.91 3 9.5 5.91 16 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/>,
    bed: <path d="M20 10V7c0-1.1-.9-2-2-2H4c-1.1 0-2 .9-2 2v3c-1.1 0-2 .9-2 2v5h1.33L2 19h2l.67-2h10.67L16 19h2l.67-2H20v-5c0-1.1-.9-2-2-2zM11 10H4V7h7v3zm9 0h-7V7h7v3z"/>,
    warning: <path d="M1 21h22L12 2 1 21zm12-3h-2v-2h2v2zm0-4h-2v-4h2v4z"/>,
    check: <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/>,
  };
  return (
    <svg viewBox="0 0 24 24" width={size} height={size} fill="currentColor" style={{ display: "inline-block", flexShrink: 0 }}>
      {icons[name] || icons.bed}
    </svg>
  );
};

// ─── Main App ────────────────────────────────────────────────────────────────
export default function App() {
  const [page, setPage] = useState("dashboard");
  const [sidebarOpen, setSidebarOpen] = useState(false);
  const [products, setProducts] = useState(SEED_PRODUCTS);
  const [customers, setCustomers] = useState(SEED_CUSTOMERS);
  const [sales, setSales] = useState(SEED_SALES);
  const [expenses, setExpenses] = useState(SEED_EXPENSES);
  const [modal, setModal] = useState(null); // { type, data }

  const totalSalesToday = sales.filter(s => s.date === "2025-06-28").reduce((a, b) => a + b.total, 0);
  const totalSalesMonth = sales.reduce((a, b) => a + b.total, 0);
  const inventoryValue = products.reduce((a, p) => a + p.price * p.stock, 0);
  const outstanding = customers.reduce((a, c) => a + c.balance, 0);
  const lowStock = products.filter(p => p.stock <= 5);

  const nav = [
    { id: "dashboard", label: "Dashboard", icon: "dashboard" },
    { id: "inventory", label: "Inventory", icon: "inventory" },
    { id: "customers", label: "Customers", icon: "customers" },
    { id: "sales", label: "Sales", icon: "sales" },
    { id: "expenses", label: "Expenses", icon: "expenses" },
    { id: "reports", label: "Reports", icon: "reports" },
    { id: "settings", label: "Settings", icon: "settings" },
  ];

  const closeModal = () => setModal(null);

  return (
    <div style={S.root}>
      <style>{CSS}</style>

      {/* Sidebar */}
      <aside style={{ ...S.sidebar, ...(sidebarOpen ? S.sidebarOpen : {}) }}>
        <div style={S.brand}>
          <Icon name="bed" size={28} />
          <div>
            <div style={S.brandName}>Smart Design</div>
            <div style={S.brandSub}>Bed Shop</div>
          </div>
        </div>
        <nav style={S.navList}>
          {nav.map(n => (
            <button key={n.id} onClick={() => { setPage(n.id); setSidebarOpen(false); }}
              style={{ ...S.navItem, ...(page === n.id ? S.navActive : {}) }}>
              <Icon name={n.icon} size={18} />
              <span>{n.label}</span>
            </button>
          ))}
        </nav>
        <div style={S.sidebarFooter}>Smart Design © 2025</div>
      </aside>

      {sidebarOpen && <div style={S.overlay} onClick={() => setSidebarOpen(false)} />}

      {/* Main */}
      <div style={S.main}>
        {/* Topbar */}
        <header style={S.topbar}>
          <button style={S.hamburger} onClick={() => setSidebarOpen(o => !o)}>
            <span /><span /><span />
          </button>
          <h1 style={S.pageTitle}>{nav.find(n => n.id === page)?.label}</h1>
          <div style={S.topRight}>
            <span style={S.dateChip}>{new Date().toLocaleDateString("en-ZA", { day: "numeric", month: "short", year: "numeric" })}</span>
          </div>
        </header>

        <main style={S.content}>
          {page === "dashboard" && <Dashboard {...{ totalSalesToday, totalSalesMonth, inventoryValue, outstanding, lowStock, customers, sales, setPage, setModal }} />}
          {page === "inventory" && <Inventory products={products} setProducts={setProducts} modal={modal} setModal={setModal} closeModal={closeModal} />}
          {page === "customers" && <Customers customers={customers} setCustomers={setCustomers} modal={modal} setModal={setModal} closeModal={closeModal} />}
          {page === "sales" && <Sales sales={sales} setSales={setSales} products={products} setProducts={setProducts} customers={customers} setCustomers={setCustomers} modal={modal} setModal={setModal} closeModal={closeModal} />}
          {page === "expenses" && <Expenses expenses={expenses} setExpenses={setExpenses} modal={modal} setModal={setModal} closeModal={closeModal} />}
          {page === "reports" && <Reports sales={sales} expenses={expenses} products={products} customers={customers} />}
          {page === "settings" && <Settings />}
        </main>
      </div>
    </div>
  );
}

// ─── Dashboard ───────────────────────────────────────────────────────────────
function Dashboard({ totalSalesToday, totalSalesMonth, inventoryValue, outstanding, lowStock, customers, sales, setPage }) {
  const cards = [
    { label: "Today's Sales", value: `R ${totalSalesToday.toLocaleString()}`, icon: "sales", color: "#1a56db" },
    { label: "Monthly Sales", value: `R ${totalSalesMonth.toLocaleString()}`, icon: "reports", color: "#0e9f6e" },
    { label: "Inventory Value", value: `R ${inventoryValue.toLocaleString()}`, icon: "inventory", color: "#7e3af2" },
    { label: "Outstanding", value: `R ${outstanding.toLocaleString()}`, icon: "customers", color: "#e3a008" },
  ];

  return (
    <div>
      {/* Stat Cards */}
      <div style={S.cardGrid}>
        {cards.map(c => (
          <div key={c.label} style={{ ...S.statCard, borderTop: `4px solid ${c.color}` }}>
            <div style={{ ...S.statIcon, background: c.color + "22", color: c.color }}>
              <Icon name={c.icon} size={24} />
            </div>
            <div>
              <div style={S.statValue}>{c.value}</div>
              <div style={S.statLabel}>{c.label}</div>
            </div>
          </div>
        ))}
      </div>

      <div style={S.twoCol}>
        {/* Recent Sales */}
        <div style={S.panel}>
          <div style={S.panelHead}><span>Recent Sales</span><button className="btn-link" onClick={() => setPage("sales")}>View all</button></div>
          <table style={S.table}>
            <thead><tr>{["Date", "Customer", "Product", "Total"].map(h => <th key={h} style={S.th}>{h}</th>)}</tr></thead>
            <tbody>
              {sales.slice(0, 5).map(s => (
                <tr key={s.id} style={S.tr}>
                  <td style={S.td}>{s.date}</td>
                  <td style={S.td}>{s.customer}</td>
                  <td style={S.td}>{s.product}</td>
                  <td style={S.td}><span style={S.badge}>{fmt(s.total)}</span></td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>

        {/* Low Stock */}
        <div style={S.panel}>
          <div style={S.panelHead}><span>Low Stock Alert</span><span style={{ ...S.badge, background: "#fee2e2", color: "#dc2626" }}>{lowStock.length} items</span></div>
          {lowStock.length === 0 ? <p style={S.empty}>All stock levels are healthy.</p> : (
            lowStock.map(p => (
              <div key={p.id} style={S.alertRow}>
                <Icon name="warning" size={16} />
                <span style={{ flex: 1 }}>{p.name}</span>
                <span style={{ ...S.badge, background: "#fef3c7", color: "#92400e" }}>{p.stock} left</span>
              </div>
            ))
          )}

          <div style={{ marginTop: 20, borderTop: "1px solid #e5e7eb", paddingTop: 16 }}>
            <div style={S.panelHead}><span>Outstanding Accounts</span></div>
            {customers.filter(c => c.balance > 0).map(c => (
              <div key={c.id} style={S.alertRow}>
                <Icon name="customers" size={16} />
                <span style={{ flex: 1 }}>{c.name}</span>
                <span style={{ ...S.badge, background: "#fee2e2", color: "#dc2626" }}>{fmt(c.balance)}</span>
              </div>
            ))}
          </div>
        </div>
      </div>
    </div>
  );
}

// ─── Inventory ───────────────────────────────────────────────────────────────
function Inventory({ products, setProducts, modal, setModal, closeModal }) {
  const [search, setSearch] = useState("");
  const filtered = products.filter(p => p.name.toLowerCase().includes(search.toLowerCase()) || p.category.toLowerCase().includes(search.toLowerCase()));

  const save = (data) => {
    if (data.id) setProducts(ps => ps.map(p => p.id === data.id ? data : p));
    else setProducts(ps => [...ps, { ...data, id: Date.now() }]);
    closeModal();
  };
  const del = (id) => { if (confirm("Delete this product?")) setProducts(ps => ps.filter(p => p.id !== id)); };

  return (
    <div>
      <div style={S.toolbar}>
        <div style={S.searchBox}><Icon name="search" size={18} /><input placeholder="Search products…" value={search} onChange={e => setSearch(e.target.value)} style={S.searchInput} /></div>
        <button style={S.btnPrimary} onClick={() => setModal({ type: "product", data: null })}>
          <Icon name="plus" size={16} /> Add Product
        </button>
      </div>
      <div style={S.panel}>
        <table style={S.table}>
          <thead><tr>{["SKU", "Name", "Category", "Cost", "Price", "Stock", "Actions"].map(h => <th key={h} style={S.th}>{h}</th>)}</tr></thead>
          <tbody>
            {filtered.map(p => (
              <tr key={p.id} style={S.tr}>
                <td style={S.td}><span style={{ fontFamily: "monospace", fontSize: 12 }}>{p.sku}</span></td>
                <td style={S.td}><strong>{p.name}</strong></td>
                <td style={S.td}><span style={S.chip}>{p.category}</span></td>
                <td style={S.td}>{fmt(p.cost)}</td>
                <td style={S.td}>{fmt(p.price)}</td>
                <td style={S.td}>
                  <span style={{ ...S.badge, background: p.stock <= 5 ? "#fee2e2" : "#d1fae5", color: p.stock <= 5 ? "#dc2626" : "#065f46" }}>{p.stock}</span>
                </td>
                <td style={S.td}>
                  <button style={S.iconBtn} onClick={() => setModal({ type: "product", data: p })}><Icon name="edit" size={16} /></button>
                  <button style={{ ...S.iconBtn, color: "#dc2626" }} onClick={() => del(p.id)}><Icon name="trash" size={16} /></button>
                </td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
      {modal?.type === "product" && <ProductModal data={modal.data} onSave={save} onClose={closeModal} />}
    </div>
  );
}

function ProductModal({ data, onSave, onClose }) {
  const [form, setForm] = useState(data || { name: "", category: "Beds", sku: "", cost: "", price: "", stock: "" });
  const set = (k, v) => setForm(f => ({ ...f, [k]: v }));
  const cats = ["Beds", "Mattresses", "Headboards", "Accessories"];
  return (
    <Modal title={data ? "Edit Product" : "Add Product"} onClose={onClose}>
      <FormRow label="Name"><input style={S.input} value={form.name} onChange={e => set("name", e.target.value)} /></FormRow>
      <FormRow label="SKU"><input style={S.input} value={form.sku} onChange={e => set("sku", e.target.value)} /></FormRow>
      <FormRow label="Category">
        <select style={S.input} value={form.category} onChange={e => set("category", e.target.value)}>
          {cats.map(c => <option key={c}>{c}</option>)}
        </select>
      </FormRow>
      <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr 1fr", gap: 12 }}>
        <FormRow label="Cost (R)"><input style={S.input} type="number" value={form.cost} onChange={e => set("cost", +e.target.value)} /></FormRow>
        <FormRow label="Price (R)"><input style={S.input} type="number" value={form.price} onChange={e => set("price", +e.target.value)} /></FormRow>
        <FormRow label="Stock"><input style={S.input} type="number" value={form.stock} onChange={e => set("stock", +e.target.value)} /></FormRow>
      </div>
      <button style={{ ...S.btnPrimary, width: "100%", marginTop: 8 }} onClick={() => onSave(form)}>
        <Icon name="check" size={16} /> Save Product
      </button>
    </Modal>
  );
}

// ─── Customers ───────────────────────────────────────────────────────────────
function Customers({ customers, setCustomers, modal, setModal, closeModal }) {
  const [search, setSearch] = useState("");
  const filtered = customers.filter(c => c.name.toLowerCase().includes(search.toLowerCase()) || c.phone.includes(search));

  const save = (data) => {
    if (data.id) setCustomers(cs => cs.map(c => c.id === data.id ? data : c));
    else setCustomers(cs => [...cs, { ...data, id: Date.now(), balance: 0 }]);
    closeModal();
  };
  const del = (id) => { if (confirm("Delete this customer?")) setCustomers(cs => cs.filter(c => c.id !== id)); };

  return (
    <div>
      <div style={S.toolbar}>
        <div style={S.searchBox}><Icon name="search" size={18} /><input placeholder="Search customers…" value={search} onChange={e => setSearch(e.target.value)} style={S.searchInput} /></div>
        <button style={S.btnPrimary} onClick={() => setModal({ type: "customer", data: null })}>
          <Icon name="plus" size={16} /> Add Customer
        </button>
      </div>
      <div style={S.panel}>
        <table style={S.table}>
          <thead><tr>{["Name", "Phone", "Email", "Address", "Balance", "Actions"].map(h => <th key={h} style={S.th}>{h}</th>)}</tr></thead>
          <tbody>
            {filtered.map(c => (
              <tr key={c.id} style={S.tr}>
                <td style={S.td}><strong>{c.name}</strong></td>
                <td style={S.td}>{c.phone}</td>
                <td style={S.td}>{c.email}</td>
                <td style={S.td}>{c.address}</td>
                <td style={S.td}><span style={{ ...S.badge, background: c.balance > 0 ? "#fee2e2" : "#d1fae5", color: c.balance > 0 ? "#dc2626" : "#065f46" }}>{fmt(c.balance)}</span></td>
                <td style={S.td}>
                  <button style={S.iconBtn} onClick={() => setModal({ type: "customer", data: c })}><Icon name="edit" size={16} /></button>
                  <button style={{ ...S.iconBtn, color: "#dc2626" }} onClick={() => del(c.id)}><Icon name="trash" size={16} /></button>
                </td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
      {modal?.type === "customer" && <CustomerModal data={modal.data} onSave={save} onClose={closeModal} />}
    </div>
  );
}

function CustomerModal({ data, onSave, onClose }) {
  const [form, setForm] = useState(data || { name: "", phone: "", email: "", address: "" });
  const set = (k, v) => setForm(f => ({ ...f, [k]: v }));
  return (
    <Modal title={data ? "Edit Customer" : "Add Customer"} onClose={onClose}>
      <FormRow label="Full Name"><input style={S.input} value={form.name} onChange={e => set("name", e.target.value)} /></FormRow>
      <FormRow label="Phone"><input style={S.input} value={form.phone} onChange={e => set("phone", e.target.value)} /></FormRow>
      <FormRow label="Email"><input style={S.input} value={form.email} onChange={e => set("email", e.target.value)} /></FormRow>
      <FormRow label="Address"><input style={S.input} value={form.address} onChange={e => set("address", e.target.value)} /></FormRow>
      <button style={{ ...S.btnPrimary, width: "100%", marginTop: 8 }} onClick={() => onSave(form)}>
        <Icon name="check" size={16} /> Save Customer
      </button>
    </Modal>
  );
}

// ─── Sales ───────────────────────────────────────────────────────────────────
function Sales({ sales, setSales, products, setProducts, customers, setCustomers, modal, setModal, closeModal }) {
  const save = (data) => {
    setSales(ss => [{ ...data, id: Date.now() }, ...ss]);
    // Deduct stock
    setProducts(ps => ps.map(p => p.name === data.product ? { ...p, stock: Math.max(0, p.stock - data.qty) } : p));
    // Update customer balance if account
    if (data.method === "Account") {
      setCustomers(cs => cs.map(c => c.name === data.customer ? { ...c, balance: c.balance + (data.total - data.paid) } : c));
    }
    closeModal();
  };

  return (
    <div>
      <div style={S.toolbar}>
        <span style={{ color: "#6b7280", fontSize: 14 }}>{sales.length} sales recorded</span>
        <button style={S.btnPrimary} onClick={() => setModal({ type: "sale", data: null })}>
          <Icon name="plus" size={16} /> New Sale
        </button>
      </div>
      <div style={S.panel}>
        <table style={S.table}>
          <thead><tr>{["Date", "Customer", "Product", "Qty", "Total", "Paid", "Method"].map(h => <th key={h} style={S.th}>{h}</th>)}</tr></thead>
          <tbody>
            {sales.map(s => (
              <tr key={s.id} style={S.tr}>
                <td style={S.td}>{s.date}</td>
                <td style={S.td}>{s.customer}</td>
                <td style={S.td}>{s.product}</td>
                <td style={S.td}>{s.qty}</td>
                <td style={S.td}><strong>{fmt(s.total)}</strong></td>
                <td style={S.td}>{fmt(s.paid)}</td>
                <td style={S.td}><span style={{ ...S.chip, background: s.method === "Cash" ? "#d1fae5" : s.method === "Card" ? "#dbeafe" : "#fef3c7" }}>{s.method}</span></td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
      {modal?.type === "sale" && <SaleModal products={products} customers={customers} onSave={save} onClose={closeModal} />}
    </div>
  );
}

function SaleModal({ products, customers, onSave, onClose }) {
  const [form, setForm] = useState({ date: today(), customer: "Walk-in", product: products[0]?.name || "", qty: 1, paid: 0, method: "Cash" });
  const set = (k, v) => setForm(f => ({ ...f, [k]: v }));
  const selectedProduct = products.find(p => p.name === form.product);
  const total = selectedProduct ? selectedProduct.price * form.qty : 0;

  return (
    <Modal title="New Sale" onClose={onClose}>
      <FormRow label="Date"><input style={S.input} type="date" value={form.date} onChange={e => set("date", e.target.value)} /></FormRow>
      <FormRow label="Customer">
        <select style={S.input} value={form.customer} onChange={e => set("customer", e.target.value)}>
          <option>Walk-in</option>
          {customers.map(c => <option key={c.id}>{c.name}</option>)}
        </select>
      </FormRow>
      <FormRow label="Product">
        <select style={S.input} value={form.product} onChange={e => set("product", e.target.value)}>
          {products.map(p => <option key={p.id}>{p.name}</option>)}
        </select>
      </FormRow>
      <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 12 }}>
        <FormRow label="Qty"><input style={S.input} type="number" min={1} value={form.qty} onChange={e => set("qty", +e.target.value)} /></FormRow>
        <FormRow label="Payment Method">
          <select style={S.input} value={form.method} onChange={e => set("method", e.target.value)}>
            {["Cash", "Card", "Account"].map(m => <option key={m}>{m}</option>)}
          </select>
        </FormRow>
      </div>
      <FormRow label="Amount Paid (R)"><input style={S.input} type="number" value={form.paid} onChange={e => set("paid", +e.target.value)} /></FormRow>
      <div style={{ background: "#f0f7ff", borderRadius: 10, padding: "12px 16px", marginBottom: 12 }}>
        <div style={{ display: "flex", justifyContent: "space-between" }}>
          <span style={{ color: "#374151" }}>Total</span>
          <strong style={{ color: "#1a56db", fontSize: 18 }}>{fmt(total)}</strong>
        </div>
        {form.method === "Account" && total - form.paid > 0 && (
          <div style={{ display: "flex", justifyContent: "space-between", marginTop: 4 }}>
            <span style={{ color: "#dc2626", fontSize: 13 }}>Balance due</span>
            <span style={{ color: "#dc2626", fontWeight: 700 }}>{fmt(total - form.paid)}</span>
          </div>
        )}
      </div>
      <button style={{ ...S.btnPrimary, width: "100%", marginTop: 8 }} onClick={() => onSave({ ...form, total, qty: form.qty })}>
        <Icon name="check" size={16} /> Record Sale
      </button>
    </Modal>
  );
}

// ─── Expenses ────────────────────────────────────────────────────────────────
function Expenses({ expenses, setExpenses, modal, setModal, closeModal }) {
  const total = expenses.reduce((a, e) => a + e.amount, 0);
  const save = (data) => {
    setExpenses(es => [{ ...data, id: Date.now() }, ...es]);
    closeModal();
  };
  const del = (id) => { if (confirm("Delete expense?")) setExpenses(es => es.filter(e => e.id !== id)); };

  return (
    <div>
      <div style={S.toolbar}>
        <span style={{ ...S.badge, background: "#fee2e2", color: "#dc2626", fontSize: 13 }}>Total: {fmt(total)}</span>
        <button style={S.btnPrimary} onClick={() => setModal({ type: "expense", data: null })}>
          <Icon name="plus" size={16} /> Add Expense
        </button>
      </div>
      <div style={S.panel}>
        <table style={S.table}>
          <thead><tr>{["Date", "Category", "Description", "Amount", ""].map(h => <th key={h} style={S.th}>{h}</th>)}</tr></thead>
          <tbody>
            {expenses.map(e => (
              <tr key={e.id} style={S.tr}>
                <td style={S.td}>{e.date}</td>
                <td style={S.td}><span style={S.chip}>{e.category}</span></td>
                <td style={S.td}>{e.description}</td>
                <td style={S.td}><strong style={{ color: "#dc2626" }}>{fmt(e.amount)}</strong></td>
                <td style={S.td}><button style={{ ...S.iconBtn, color: "#dc2626" }} onClick={() => del(e.id)}><Icon name="trash" size={16} /></button></td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
      {modal?.type === "expense" && <ExpenseModal onSave={save} onClose={closeModal} />}
    </div>
  );
}

function ExpenseModal({ onSave, onClose }) {
  const [form, setForm] = useState({ date: today(), category: "Rent", description: "", amount: "" });
  const set = (k, v) => setForm(f => ({ ...f, [k]: v }));
  const cats = ["Rent", "Electricity", "Fuel", "Salaries", "Repairs", "General"];
  return (
    <Modal title="Add Expense" onClose={onClose}>
      <FormRow label="Date"><input style={S.input} type="date" value={form.date} onChange={e => set("date", e.target.value)} /></FormRow>
      <FormRow label="Category">
        <select style={S.input} value={form.category} onChange={e => set("category", e.target.value)}>
          {cats.map(c => <option key={c}>{c}</option>)}
        </select>
      </FormRow>
      <FormRow label="Description"><input style={S.input} value={form.description} onChange={e => set("description", e.target.value)} /></FormRow>
      <FormRow label="Amount (R)"><input style={S.input} type="number" value={form.amount} onChange={e => set("amount", +e.target.value)} /></FormRow>
      <button style={{ ...S.btnPrimary, width: "100%", marginTop: 8 }} onClick={() => onSave(form)}>
        <Icon name="check" size={16} /> Save Expense
      </button>
    </Modal>
  );
}

// ─── Reports ─────────────────────────────────────────────────────────────────
function Reports({ sales, expenses, products, customers }) {
  const totalRevenue = sales.reduce((a, s) => a + s.total, 0);
  const totalExpenses = expenses.reduce((a, e) => a + e.amount, 0);
  const totalCost = sales.reduce((a, s) => {
    const p = products.find(pr => pr.name === s.product);
    return a + (p ? p.cost * s.qty : 0);
  }, 0);
  const grossProfit = totalRevenue - totalCost;
  const netProfit = grossProfit - totalExpenses;

  const byMethod = ["Cash", "Card", "Account"].map(m => ({
    method: m,
    total: sales.filter(s => s.method === m).reduce((a, s) => a + s.total, 0),
    count: sales.filter(s => s.method === m).length,
  }));

  const byCategory = [...new Set(expenses.map(e => e.category))].map(cat => ({
    cat,
    total: expenses.filter(e => e.category === cat).reduce((a, e) => a + e.amount, 0),
  }));

  return (
    <div>
      {/* Profit Summary */}
      <div style={S.cardGrid}>
        {[
          { label: "Total Revenue", value: fmt(totalRevenue), color: "#1a56db" },
          { label: "Cost of Goods", value: fmt(totalCost), color: "#7e3af2" },
          { label: "Gross Profit", value: fmt(grossProfit), color: "#0e9f6e" },
          { label: "Net Profit", value: fmt(netProfit), color: netProfit >= 0 ? "#0e9f6e" : "#dc2626" },
        ].map(c => (
          <div key={c.label} style={{ ...S.statCard, borderTop: `4px solid ${c.color}` }}>
            <div style={{ fontSize: 22, fontWeight: 800, color: c.color }}>{c.value}</div>
            <div style={S.statLabel}>{c.label}</div>
          </div>
        ))}
      </div>

      <div style={S.twoCol}>
        <div style={S.panel}>
          <div style={S.panelHead}><span>Sales by Payment Method</span></div>
          <table style={S.table}>
            <thead><tr>{["Method", "Sales", "Total"].map(h => <th key={h} style={S.th}>{h}</th>)}</tr></thead>
            <tbody>{byMethod.map(m => (
              <tr key={m.method} style={S.tr}>
                <td style={S.td}><span style={S.chip}>{m.method}</span></td>
                <td style={S.td}>{m.count}</td>
                <td style={S.td}><strong>{fmt(m.total)}</strong></td>
              </tr>
            ))}</tbody>
          </table>
        </div>
        <div style={S.panel}>
          <div style={S.panelHead}><span>Expenses by Category</span></div>
          <table style={S.table}>
            <thead><tr>{["Category", "Total"].map(h => <th key={h} style={S.th}>{h}</th>)}</tr></thead>
            <tbody>{byCategory.map(c => (
              <tr key={c.cat} style={S.tr}>
                <td style={S.td}><span style={S.chip}>{c.cat}</span></td>
                <td style={S.td}><strong style={{ color: "#dc2626" }}>{fmt(c.total)}</strong></td>
              </tr>
            ))}</tbody>
          </table>
        </div>
      </div>

      <div style={S.panel}>
        <div style={S.panelHead}><span>Outstanding Customer Balances</span></div>
        <table style={S.table}>
          <thead><tr>{["Customer", "Phone", "Balance"].map(h => <th key={h} style={S.th}>{h}</th>)}</tr></thead>
          <tbody>{customers.filter(c => c.balance > 0).map(c => (
            <tr key={c.id} style={S.tr}>
              <td style={S.td}><strong>{c.name}</strong></td>
              <td style={S.td}>{c.phone}</td>
              <td style={S.td}><span style={{ ...S.badge, background: "#fee2e2", color: "#dc2626" }}>{fmt(c.balance)}</span></td>
            </tr>
          ))}</tbody>
        </table>
      </div>
    </div>
  );
}

// ─── Settings ────────────────────────────────────────────────────────────────
function Settings() {
  const [form, setForm] = useState({ shopName: "Smart Design Bed Shop", phone: "031 555 0000", email: "info@smartdesign.co.za", address: "123 Bed Street, Durban", vatNo: "" });
  const set = (k, v) => setForm(f => ({ ...f, [k]: v }));
  return (
    <div style={{ maxWidth: 560 }}>
      <div style={S.panel}>
        <div style={S.panelHead}><span>Business Information</span></div>
        <FormRow label="Shop Name"><input style={S.input} value={form.shopName} onChange={e => set("shopName", e.target.value)} /></FormRow>
        <FormRow label="Phone"><input style={S.input} value={form.phone} onChange={e => set("phone", e.target.value)} /></FormRow>
        <FormRow label="Email"><input style={S.input} value={form.email} onChange={e => set("email", e.target.value)} /></FormRow>
        <FormRow label="Address"><input style={S.input} value={form.address} onChange={e => set("address", e.target.value)} /></FormRow>
        <FormRow label="VAT Number"><input style={S.input} value={form.vatNo} onChange={e => set("vatNo", e.target.value)} /></FormRow>
        <button style={S.btnPrimary}><Icon name="check" size={16} /> Save Settings</button>
      </div>
    </div>
  );
}

// ─── Shared UI Components ────────────────────────────────────────────────────
function Modal({ title, children, onClose }) {
  return (
    <div style={S.modalBackdrop}>
      <div style={S.modalBox}>
        <div style={S.modalHead}>
          <h2 style={S.modalTitle}>{title}</h2>
          <button style={S.closeBtn} onClick={onClose}><Icon name="close" size={20} /></button>
        </div>
        <div style={S.modalBody}>{children}</div>
      </div>
    </div>
  );
}

function FormRow({ label, children }) {
  return (
    <div style={{ marginBottom: 14 }}>
      <label style={S.label}>{label}</label>
      {children}
    </div>
  );
}

// ─── Styles ──────────────────────────────────────────────────────────────────
const S = {
  root: { display: "flex", minHeight: "100vh", background: "#f1f5f9", fontFamily: "'Segoe UI', system-ui, sans-serif", color: "#111827" },
  sidebar: { width: 240, background: "linear-gradient(180deg, #0f2563 0%, #1a3a8f 100%)", display: "flex", flexDirection: "column", position: "fixed", top: 0, left: 0, height: "100vh", zIndex: 200, transition: "transform .25s ease", transform: "translateX(0)" },
  sidebarOpen: { transform: "translateX(0)" },
  brand: { display: "flex", alignItems: "center", gap: 12, padding: "24px 20px 20px", color: "#f5d060", borderBottom: "1px solid rgba(255,255,255,.1)" },
  brandName: { fontWeight: 800, fontSize: 15, color: "#fff", lineHeight: 1.2 },
  brandSub: { fontSize: 11, color: "#93c5fd", textTransform: "uppercase", letterSpacing: ".08em" },
  navList: { flex: 1, overflowY: "auto", padding: "12px 12px" },
  navItem: { display: "flex", alignItems: "center", gap: 12, width: "100%", padding: "11px 14px", borderRadius: 10, border: "none", background: "transparent", color: "#bfdbfe", cursor: "pointer", fontSize: 14, fontWeight: 500, marginBottom: 2, textAlign: "left", transition: "background .15s" },
  navActive: { background: "rgba(255,255,255,.15)", color: "#fff" },
  sidebarFooter: { padding: "14px 20px", fontSize: 11, color: "rgba(255,255,255,.3)", borderTop: "1px solid rgba(255,255,255,.1)" },
  overlay: { position: "fixed", inset: 0, background: "rgba(0,0,0,.4)", zIndex: 190 },
  main: { flex: 1, marginLeft: 240, display: "flex", flexDirection: "column", minHeight: "100vh" },
  topbar: { background: "#fff", borderBottom: "1px solid #e5e7eb", padding: "0 24px", height: 64, display: "flex", alignItems: "center", gap: 16, position: "sticky", top: 0, zIndex: 100, boxShadow: "0 1px 4px rgba(0,0,0,.06)" },
  hamburger: { display: "none", flexDirection: "column", gap: 4, background: "none", border: "none", cursor: "pointer", padding: 6 },
  pageTitle: { flex: 1, fontSize: 18, fontWeight: 700, color: "#0f2563" },
  topRight: { display: "flex", alignItems: "center", gap: 12 },
  dateChip: { fontSize: 12, color: "#6b7280", background: "#f3f4f6", padding: "4px 10px", borderRadius: 20 },
  content: { flex: 1, padding: 24 },
  cardGrid: { display: "grid", gridTemplateColumns: "repeat(auto-fill, minmax(200px, 1fr))", gap: 16, marginBottom: 24 },
  statCard: { background: "#fff", borderRadius: 14, padding: "20px 20px", boxShadow: "0 1px 4px rgba(0,0,0,.07)", display: "flex", alignItems: "center", gap: 16 },
  statIcon: { width: 48, height: 48, borderRadius: 12, display: "flex", alignItems: "center", justifyContent: "center", flexShrink: 0 },
  statValue: { fontSize: 20, fontWeight: 800, color: "#111827" },
  statLabel: { fontSize: 12, color: "#6b7280", marginTop: 2 },
  twoCol: { display: "grid", gridTemplateColumns: "1fr 1fr", gap: 20, marginBottom: 20 },
  panel: { background: "#fff", borderRadius: 14, padding: 20, boxShadow: "0 1px 4px rgba(0,0,0,.07)", marginBottom: 20, overflowX: "auto" },
  panelHead: { display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 16, fontWeight: 700, color: "#0f2563", fontSize: 15 },
  table: { width: "100%", borderCollapse: "collapse" },
  th: { textAlign: "left", padding: "8px 10px", fontSize: 11, fontWeight: 700, textTransform: "uppercase", letterSpacing: ".06em", color: "#6b7280", borderBottom: "2px solid #f3f4f6" },
  tr: { transition: "background .1s" },
  td: { padding: "10px 10px", borderBottom: "1px solid #f3f4f6", fontSize: 13, verticalAlign: "middle" },
  badge: { display: "inline-block", padding: "3px 10px", borderRadius: 20, fontSize: 12, fontWeight: 600, background: "#dbeafe", color: "#1e40af" },
  chip: { display: "inline-block", padding: "3px 10px", borderRadius: 6, fontSize: 12, fontWeight: 600, background: "#f3f4f6", color: "#374151" },
  alertRow: { display: "flex", alignItems: "center", gap: 10, padding: "8px 0", borderBottom: "1px solid #f3f4f6", fontSize: 13, color: "#92400e" },
  toolbar: { display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 16, gap: 12 },
  searchBox: { display: "flex", alignItems: "center", gap: 8, background: "#fff", borderRadius: 10, padding: "8px 14px", boxShadow: "0 1px 3px rgba(0,0,0,.07)", flex: 1, maxWidth: 360, color: "#9ca3af" },
  searchInput: { border: "none", outline: "none", fontSize: 14, flex: 1, color: "#111827", background: "transparent" },
  btnPrimary: { display: "inline-flex", alignItems: "center", gap: 8, background: "linear-gradient(135deg, #1a56db, #1e3a8a)", color: "#fff", border: "none", borderRadius: 10, padding: "10px 18px", fontSize: 14, fontWeight: 600, cursor: "pointer", boxShadow: "0 2px 8px rgba(26,86,219,.3)" },
  iconBtn: { background: "none", border: "none", cursor: "pointer", color: "#1a56db", padding: 4, borderRadius: 6, display: "inline-flex" },
  modalBackdrop: { position: "fixed", inset: 0, background: "rgba(0,0,0,.5)", zIndex: 1000, display: "flex", alignItems: "center", justifyContent: "center", padding: 16 },
  modalBox: { background: "#fff", borderRadius: 16, width: "100%", maxWidth: 500, boxShadow: "0 20px 60px rgba(0,0,0,.3)", maxHeight: "90vh", overflowY: "auto" },
  modalHead: { display: "flex", justifyContent: "space-between", alignItems: "center", padding: "20px 24px 16px", borderBottom: "1px solid #f3f4f6" },
  modalTitle: { fontSize: 18, fontWeight: 700, color: "#0f2563" },
  modalBody: { padding: "20px 24px 24px" },
  closeBtn: { background: "none", border: "none", cursor: "pointer", color: "#6b7280", display: "flex", padding: 4, borderRadius: 6 },
  label: { display: "block", fontSize: 12, fontWeight: 600, color: "#374151", marginBottom: 6, textTransform: "uppercase", letterSpacing: ".04em" },
  input: { width: "100%", padding: "10px 12px", border: "1.5px solid #e5e7eb", borderRadius: 8, fontSize: 14, color: "#111827", outline: "none", boxSizing: "border-box", background: "#fafafa" },
  empty: { color: "#9ca3af", fontSize: 13, textAlign: "center", padding: "20px 0" },
};

const CSS = `
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { background: #f1f5f9; }
  button:hover { opacity: .88; }
  .btn-link { background: none; border: none; color: #1a56db; cursor: pointer; font-size: 13px; font-weight: 600; }
  tr:hover td { background: #f8faff; }
  input:focus, select:focus { border-color: #1a56db !important; }
  @media (max-width: 768px) {
    .sidebar { transform: translateX(-100%) !important; }
    .sidebar.open { transform: translateX(0) !important; }
    .main { margin-left: 0 !important; }
    .hamburger { display: flex !important; }
    .two-col { grid-template-columns: 1fr !important; }
    .card-grid { grid-template-columns: 1fr 1fr !important; }
  }
`;
