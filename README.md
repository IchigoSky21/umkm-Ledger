# 🏪 TokoKita — UMKM Financial & Inventory Tracker

TokoKita is a lightweight, client-side web application for small and medium-sized businesses (UMKM) to manage daily sales, expenses, inventory, and basic financial metrics directly in the browser.

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![Vanilla JS](https://img.shields.io/badge/Vanilla%20JS-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![PWA](https://img.shields.io/badge/PWA-Ready-5A0FC8?style=for-the-badge&logo=pwa&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps)

## 🌐 Live Demo

**Try TokoKita:**

https://ichigosky21.github.io/UMKM-Ledger/

**Project background / design reference:**

https://canva.link/qb2l4e7bxbjay0u

---

## 📖 Overview

TokoKita is designed as a simple business operations dashboard for UMKM owners who need a practical way to record transactions and monitor inventory without setting up a backend or database.

The application runs primarily on the client side and stores transaction, inventory, and theme data in the browser's `localStorage`. It also includes a web app manifest and a service worker for PWA-related functionality and asset caching.

The current implementation focuses on three main areas:

- **Dashboard** — daily revenue, sales count, active inventory valuation, monthly revenue progress toward a fixed BEP target, and today's transaction feed.
- **Transactions** — transaction history with date/type filters, deletion, and Excel export.
- **Inventory** — stock management, search, low-stock filtering, margin calculation, item creation/editing/deletion, and Excel export.

---

## ✨ Key Features

### 📊 Financial Dashboard

- Tracks today's revenue and number of sales.
- Calculates the current value of active inventory using COGS × stock quantity.
- Displays monthly revenue progress against the application's fixed **Rp 5,000,000** BEP target.
- Shows the day's transaction activity in a compact ledger feed.

### ⚡ Quick Transaction Entry

- Records either **Sale (Income)** or **Restock (Expense)** transactions.
- Automatically calculates the transaction amount from the selected item's selling price or COGS and quantity.
- Supports **QRIS / Digital Pay** and **Cash** as payment channels.
- Prevents sales from being recorded when available stock is insufficient.

### 📦 Inventory Management

- Starts with sample inventory for **Nasi, Tahu, and Tempe** when no saved inventory exists.
- Stores stock quantity, minimum stock threshold, COGS, and selling price for each item.
- Calculates gross margin percentage from COGS and selling price.
- Highlights inventory as **Sufficient**, **Low**, or **Empty**.
- Supports adding, editing, deleting, searching, and filtering inventory items.

### 📑 Excel Export

The application uses the browser-based **SheetJS** library to export data without a backend server:

- Transaction history → `.xlsx`
- Inventory data → `.xlsx`

### 🌙 Theme Support

- Light and dark modes are available.
- The selected theme is persisted in `localStorage`.

### 📱 PWA Components

The repository includes:

- `manifest.json` for web app metadata.
- `sw.js` for caching the application's core files.
- A standalone-style manifest configuration suitable for an installable web app.

> **Implementation note:** the repository currently contains the PWA manifest and service worker, but the current `app.js` does not explicitly register `sw.js`. Therefore, this README does not claim that full offline/PWA behavior is automatically active in every deployment.

---

## 🧠 How It Works

TokoKita is intentionally simple and does not require a backend database.

```text
User Input
    │
    ├── Transactions ──────┐
    │                      │
    └── Inventory ─────────┤
                           ▼
                     localStorage
                           │
                           ▼
                    Dashboard / Tables
                           │
                           ├── Calculations
                           └── Excel Export
```

### Transaction flow

1. Select a transaction type.
2. Select an inventory item and enter the quantity.
3. The application calculates the amount using the item's selling price or COGS.
4. The transaction is stored in `localStorage`.
5. Inventory quantity is updated automatically.
6. Dashboard and transaction views are refreshed.

### Inventory flow

Inventory records contain:

- Item name
- Current stock
- Minimum stock threshold
- COGS / capital cost
- Selling price

The application uses these values to calculate stock status, inventory valuation, and gross margin.

---

## 🛠️ Tech Stack

| Technology | Purpose |
| --- | --- |
| HTML5 | Application structure and UI markup |
| CSS3 | Responsive layout, components, and theme styling |
| Vanilla JavaScript | Application logic and state management |
| LocalStorage API | Client-side persistence |
| SheetJS (`xlsx`) | `.xlsx` export functionality |
| Service Worker API | Application-shell caching |
| Web App Manifest | PWA metadata |
| Google Fonts (Poppins) | Typography |
| Boxicons | Interface icons |

The project has **no build system, framework, or package manager**. Its frontend files can be served as a static website.

---

## 📂 Project Structure

```text
UMKM-Ledger/
├── index.html                 # Main application UI
├── styles.css                 # Responsive styling and theme definitions
├── app.js                     # State management and application logic
├── sw.js                      # Service worker and cache configuration
├── manifest.json              # Web app / PWA metadata
├── figma_initial_prototype.fig # Initial UI/UX design prototype
└── README.md                  # Project documentation
```

---

## 🚀 Run Locally

Because TokoKita is a static client-side application, no backend setup is required.

### Option 1 — Open the HTML file

Clone the repository and open `index.html` in a modern browser.

```bash
git clone https://github.com/IchigoSky21/UMKM-Ledger.git
cd UMKM-Ledger
```

Then open `index.html`.

### Option 2 — Use a local static server

For a more representative web environment, serve the project with any static HTTP server. For example, with Python:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

Using a local server is also preferable when testing browser features such as service workers.

---

## 💾 Data Storage

TokoKita stores application data locally in the browser using `localStorage`.

The current implementation uses the following storage keys:

- `umkm_transactions` — saved transaction records.
- `umkm_inventory` — saved inventory data.
- `theme` — saved light/dark mode preference.

This means data is tied to the browser/device where it was created. There is currently no user account system, cloud synchronization, or shared database.

Clearing the browser's site data can remove locally stored application data.

---

## 📤 Exported Data

### Transactions

The transaction export contains:

- Date
- Time
- Type
- Item
- Quantity
- Amount
- Payment channel

### Inventory

The inventory export contains:

- Item name
- Current stock
- Minimum stock limit
- COGS
- Selling price

Exported files are generated directly in the browser using SheetJS.

---

## ⚠️ Current Limitations

The current repository is a lightweight frontend prototype rather than a production accounting system. In particular:

- Data is stored only in browser `localStorage`.
- There is no authentication or multi-user access control.
- There is no backend database or cloud synchronization.
- The BEP target is currently hard-coded to **Rp 5,000,000** in `app.js`.
- The transaction deletion logic restores stock based on the stored transaction record.
- Excel export is generated locally in the browser.
- The service worker exists, but it is not explicitly registered by the current application code.

For real business use, additional validation, authentication, backup, data integrity controls, and a persistent backend would be appropriate.

---

## 🔮 Possible Improvements

Potential future improvements include:

- Add explicit service-worker registration and install/update handling.
- Introduce configurable BEP targets.
- Add profit and expense analytics beyond the current revenue-based BEP progress.
- Add data import and backup/restore functionality.
- Add charts for sales and inventory trends.
- Add authentication and cloud synchronization.
- Introduce a backend database for multi-device usage.
- Add stronger validation and audit history for financial records.

---

## 📄 License

No `LICENSE` file is currently included in the repository. Therefore, the repository should not be assumed to be released under a specific open-source license.

If this project is intended for public reuse, adding an explicit license would make the usage and contribution terms clearer.

---

If you find the project useful or want to explore the implementation, feel free to inspect the source code and experiment with the application.
