# Youthinity Book — Design System & Application UI/UX Specification

> **Version:** 1.0  
> **Status:** Implementation-ready design direction  
> **Product:** Youthinity Book — GST billing, inventory, POS, accounting and bookkeeping SaaS  
> **Primary surfaces:** Web application (desktop-first workflows, fully responsive)  
> **Visual direction:** Dark navigation + light workspace  
> **Design reference:** Linear's product-focused hierarchy, restrained accent usage, fine borders and clear typography, adapted for business finance workflows. This is an independent design system, not a copy of Linear.

---

## 1. Product design goals

Youthinity Book should feel like dependable business software: calm, precise, fast and understandable to shop owners, accountants, cashiers and business teams. It must support dense financial data without becoming visually noisy.

### Core principles

1. **Clarity over decoration.** Amounts, tax rates, due dates, stock quantities and transaction states must be easy to scan.
2. **Fast paths for frequent work.** Creating a sale, recording a payment, finding a product and printing an invoice should require minimal navigation.
3. **Visible financial consequences.** Totals, tax splits, outstanding balances and stock changes should be previewed before a transaction is committed.
4. **Safe by default.** Destructive, irreversible or accounting-impacting actions require clear confirmation and appropriate permissions.
5. **Offline honesty.** Show whether data is local, synced, pending or failed. Never imply a transaction reached the server when it has not.
6. **Progressive disclosure.** Everyday workflows stay simple; advanced accounting, GST and inventory options remain available without overwhelming first-time users.
7. **Consistent across roles.** Navigation, labels, statuses and controls should remain predictable for owners, managers, cashiers, inventory staff and CAs.

### Product personality

- Professional, grounded, efficient, trustworthy.
- Helpful rather than overly playful.
- Plain-language labels; use accounting terminology where it is necessary and explain uncommon terms inline.
- Avoid decorative gradients, oversized illustrations, excessive rounded cards, and arbitrary charts.

### Main user roles

- **Business owner / Admin:** overview, billing, reports, settings, subscription, team.
- **Store manager:** sales, purchases, stock, parties, reports within granted permissions.
- **POS cashier / Salesman:** rapid checkout, customer lookup, payment and receipt.
- **Inventory manager:** products, stock movements, warehouses, batches, expiry, serial numbers.
- **External CA:** assigned businesses, ledgers, reports, GST exports and audit history.
- **Delivery agent:** only assigned delivery and order information.

---

## 2. Information architecture

### Global shell

- **Left sidebar:** persistent primary navigation on desktop; collapsible to icon rail; drawer on mobile.
- **Top bar:** current business switcher, global search / command menu, sync state, notifications, help, profile.
- **Workspace:** page title, breadcrumb where useful, primary action, page-level filters and content.
- **Contextual action area:** sticky totals/action bar for long forms and billing screens.
- **Mobile navigation:** drawer plus optional bottom navigation for high-frequency tasks; never force desktop data tables into tiny unreadable layouts.

### Navigation structure

1. **Overview**
   - Dashboard
   - Activity
2. **Sales**
   - POS
   - Sales invoices
   - Quotations / estimates
   - Delivery challans
   - Sales returns / credit notes
   - Recurring invoices
3. **Purchases**
   - Purchase bills
   - Purchase orders
   - Purchase returns / debit notes
4. **Inventory**
   - Products & services
   - Stock summary
   - Stock movements
   - Warehouses / transfers
   - Barcode & labels
   - Batches & expiry
   - Serial numbers / IMEI
5. **Parties**
   - Customers
   - Suppliers
   - Party ledger
6. **Payments**
   - Receipts
   - Payment out
   - Cash & bank
   - Reconciliation
7. **Accounting**
   - Chart of accounts
   - Journal entries
   - Ledger
   - Trial balance
   - Daybook
   - Profit & loss
   - Balance sheet
   - Cash flow
   - Expenses
8. **GST & Compliance**
   - GST overview
   - GSTR-1
   - GSTR-2B reconciliation
   - GSTR-3B
   - E-invoices
   - E-way bills
   - Exports & CA reports
9. **Insights**
   - Sales reports
   - Purchase reports
   - Inventory reports
   - Receivables & payables
   - Tax reports
10. **Growth**
    - Online store
    - WhatsApp / SMS campaigns
    - Loyalty
11. **AI Bookkeeping**
    - Imports
    - Suggested matches
    - Review queue
    - History
12. **Team & Settings**
    - Team and roles
    - Business profile
    - GST / tax configuration
    - Invoice design
    - Integrations
    - Subscription & billing
    - Audit log
    - Import / migration
    - Devices & offline sync

**Navigation rules**
- Use section labels in muted text and clear icons.
- Keep the sidebar stable across routes; active state uses a pale accent tint and a narrow accent marker.
- Show counts only when actionable (e.g., pending approvals, failed sync jobs).
- Hide modules that a user cannot access; do not show dead-end links.
- Preserve current business context when navigating.
- Display business name and GST registration status in the business switcher.

---

## 3. Design tokens

Use CSS custom properties as the source of truth. Tokens are designed for a light workspace framed by a dark navigation shell.

### 3.1 Color palette

```css
:root {
  /* Brand */
  --yb-brand: #5865D9;
  --yb-brand-hover: #4653C7;
  --yb-brand-pressed: #3945B2;
  --yb-brand-soft: #EEF0FF;
  --yb-brand-border: #CCD1FF;
  --yb-focus: #6574F5;

  /* Dark application shell */
  --yb-shell: #171923;
  --yb-shell-raised: #202331;
  --yb-shell-hover: #292D3D;
  --yb-shell-active: #30364B;
  --yb-shell-border: #303444;
  --yb-shell-text: #F4F5FA;
  --yb-shell-muted: #A8ADBF;
  --yb-shell-subtle: #777F96;

  /* Light workspace */
  --yb-canvas: #F6F7FB;
  --yb-surface: #FFFFFF;
  --yb-surface-subtle: #FAFBFE;
  --yb-surface-hover: #F2F4FA;
  --yb-border: #E3E6EF;
  --yb-border-strong: #C9CEDC;

  /* Text */
  --yb-text: #1D2233;
  --yb-text-secondary: #5E667A;
  --yb-text-muted: #7D8598;
  --yb-text-disabled: #A9AFBD;
  --yb-text-inverse: #FFFFFF;

  /* Semantic */
  --yb-success: #16845B;
  --yb-success-bg: #E8F7EF;
  --yb-warning: #A66309;
  --yb-warning-bg: #FFF4DD;
  --yb-danger: #C43D4B;
  --yb-danger-bg: #FDECEF;
  --yb-info: #2367B7;
  --yb-info-bg: #EAF3FF;

  /* Data visualization — use sparingly and consistently */
  --yb-chart-1: #5865D9;
  --yb-chart-2: #16845B;
  --yb-chart-3: #D18A27;
  --yb-chart-4: #2D8DA8;
  --yb-chart-5: #8B62B4;

  /* Elevation */
  --yb-shadow-sm: 0 1px 2px rgb(25 32 54 / 5%);
  --yb-shadow-md: 0 8px 24px rgb(25 32 54 / 10%);
  --yb-shadow-popover: 0 12px 32px rgb(18 24 43 / 16%);

  /* Shape */
  --yb-radius-xs: 4px;
  --yb-radius-sm: 6px;
  --yb-radius-md: 8px;
  --yb-radius-lg: 12px;
  --yb-radius-xl: 16px;
  --yb-radius-pill: 999px;

  /* Spacing: 4px base */
  --yb-space-1: 4px;
  --yb-space-2: 8px;
  --yb-space-3: 12px;
  --yb-space-4: 16px;
  --yb-space-5: 20px;
  --yb-space-6: 24px;
  --yb-space-8: 32px;
  --yb-space-10: 40px;
  --yb-space-12: 48px;

  /* Layout */
  --yb-sidebar-width: 248px;
  --yb-sidebar-collapsed-width: 72px;
  --yb-topbar-height: 64px;
  --yb-content-max: 1600px;

  /* Motion */
  --yb-motion-fast: 120ms;
  --yb-motion-normal: 180ms;
  --yb-motion-slow: 260ms;
  --yb-ease: cubic-bezier(.2, .8, .2, 1);
}
```

### 3.2 Color usage rules

- Brand indigo is reserved for primary actions, active navigation, selected controls, links and focus indication.
- Never use brand color as the background for every card or chart.
- Green means successful / paid / in stock; amber means pending / attention; red means failed / overdue / destructive. Always pair color with text or an icon.
- Keep normal content on white surfaces. Use canvas gray to separate the workspace from panels.
- Financial tables should use neutral backgrounds and subtle separators; avoid zebra stripes unless needed for large tables.
- For printed invoices, use a separate print palette with black text, white paper and minimal accent color.

### 3.3 Typography

**Primary font:** Inter.  
**Fallback:** `Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif`.  
**Numeric data:** use tabular numerals (`font-variant-numeric: tabular-nums`) for amounts, quantities and dates.

| Token | Size / line height | Weight | Usage |
|---|---:|---:|---|
| Display | 32 / 40 px | 650 | Rare onboarding / empty-state headline |
| Page title | 24 / 32 px | 650 | Main page heading |
| Section title | 18 / 26 px | 600 | Panel or section heading |
| Card title | 15 / 22 px | 600 | Small panel heading |
| Body | 14 / 21 px | 400 | Main application copy |
| Body strong | 14 / 21 px | 550 | Table emphasis, labels |
| Small | 12 / 18 px | 400 | Helper text, metadata |
| Micro | 11 / 16 px | 500 | Dense table metadata only |
| Button | 13 / 18 px | 600 | Controls |
| Metric | 26–30 / 34 px | 650 | Dashboard figures |
| Invoice total | 24–32 px | 700 | Final amount due |
| Mono | 12 / 18 px | 450 | IDs, SKU, reference numbers |

Rules:
- Use sentence case for page titles, buttons and labels.
- Use a maximum of two font families.
- Avoid very light font weights in financial tables.
- Never communicate state using typography weight alone.
- Do not shrink essential mobile text below 12px.

### 3.4 Spacing, grid and breakpoints

- Base unit: 4px.
- Standard page padding: 28px desktop, 20px tablet, 16px mobile.
- Card padding: 20–24px desktop, 16px mobile.
- Form field gap: 16px; related fields: 8–12px.
- Section gap: 24px; major dashboard row gap: 20px.
- Content width: fluid up to 1600px.
- Desktop grid: 12 columns; tablet: 8; mobile: 4.
- Prefer `minmax(0, 1fr)` to prevent overflow in grid layouts.

| Breakpoint | Width | Behavior |
|---|---:|---|
| Mobile S | 320–374px | Single column, compact labels, key actions prioritized |
| Mobile | 375–767px | Drawer navigation, stacked panels, mobile forms |
| Tablet | 768–1023px | Collapsed sidebar, 2-column summaries where practical |
| Desktop | 1024–1439px | Full shell, standard content grid |
| Desktop XL | 1440px+ | Full shell and wider tables / multi-column panels |

### 3.5 Radius and elevation

- Inputs and buttons: 8px.
- Small status chips: 6px or pill only for compact status.
- Cards and dialogs: 12px.
- Large preview surfaces: 16px.
- Use subtle shadows only for floating menus, dialogs and drag layers.
- Cards use borders before shadows; avoid a “stack of floating cards” appearance.

---

## 4. Application shell

### 4.1 Desktop layout

```text
┌──────────────────────┬───────────────────────────────────────────────────┐
│ YOUTHINITY BOOK      │ Business ▾  Search…     Sync  Alerts  Help  User │
│──────────────────────┤───────────────────────────────────────────────────┤
│ Overview             │ Breadcrumb / Page title          [Primary action]│
│ Sales                │ Description / Filters / Tabs                     │
│ Purchases            │                                                   │
│ Inventory            │ Main content                                     │
│ Parties              │                                                   │
│ Payments             │                                                   │
│ Accounting           │                                                   │
│ GST & Compliance     │                                                   │
│ Insights              │                                                   │
│ Growth               │                                                   │
│ AI Bookkeeping       │                                                   │
│──────────────────────│                                                   │
│ Settings             │                                                   │
│ Help & support       │                                                   │
│ Trial / Plan status  │                                                   │
└──────────────────────┴───────────────────────────────────────────────────┘
```

### 4.2 Sidebar specifications

- Width: 248px expanded, 72px collapsed.
- Background: `--yb-shell`.
- Divider: `--yb-shell-border`.
- Brand area: 64px height, compact logo mark plus wordmark.
- Navigation item: 40px high, 8px radius, 12px horizontal padding.
- Icon size: 18px, consistent Lucide outline family.
- Active item: `--yb-shell-active` background, white text, 3px indigo leading marker.
- Hover item: `--yb-shell-hover`.
- Sidebar footer: plan status, help, settings and collapse control.
- In collapsed mode, provide accessible tooltips and never rely on icons alone for critical meaning.

### 4.3 Top bar

- Height: 64px; sticky on scroll.
- Surface: white with bottom border.
- Left: business switcher showing name, business type / GST state as secondary information.
- Center: global search / command menu, shortcut hint `Ctrl K` / `⌘ K`.
- Right: sync status, notifications, help, avatar menu.
- Search results grouped by customers, products, invoices, pages and actions.
- On narrow screens, reduce to business selector, search icon, sync state and profile.

### 4.4 Workspace conventions

Every standard page should have:
1. Breadcrumb only when it helps orientation.
2. Page title and one-line description (description can be omitted on familiar utility pages).
3. Primary action at top right.
4. Filters and tabs directly above the content they control.
5. Loading, empty, error and permission-denied states.
6. Keyboard focus and visible action feedback.

Use a sticky bottom action bar for long create/edit forms when the primary action would otherwise scroll out of view.

---

## 5. Component library

### 5.1 Buttons

| Variant | Style | Use |
|---|---|---|
| Primary | Brand background, white text | One main action per region: Save, Create invoice, Complete sale |
| Secondary | White, border, dark text | Cancel, Export, Preview |
| Tertiary / ghost | Transparent, text or icon | Inline actions, toolbar controls |
| Danger | Red-tinted or red solid for final destructive action | Delete, revoke access |
| Link | Brand text, no filled background | Navigation or contextual details |
| Icon-only | 36–40px square, visible tooltip | Compact table / toolbar actions |

States: default, hover, pressed, focus-visible, disabled, loading. Loading buttons preserve width and show progress; prevent duplicate submission. Avoid multiple primary buttons in the same visual region.

### 5.2 Inputs and forms

- Height: 40px desktop; minimum 44px on touch.
- Border: `--yb-border-strong`; focus: 2px brand ring with offset.
- Labels remain visible above fields; do not use placeholder as the only label.
- Helper text appears under the field; validation appears under the helper area and is associated programmatically.
- Currency fields align numeric text right; show currency code/symbol clearly.
- GSTIN, HSN/SAC, SKU, invoice number and phone fields may use monospace only where it improves scanability.
- Use autocomplete and input masks carefully; allow paste and correction.
- Inline validation occurs on blur or submit, not aggressively on every keystroke.
- Preserve entered values if server validation fails.

### 5.3 Tables

Tables are a core interface and must remain readable at high data density.

- Row height: 48px standard; 40px dense mode; 56px for multiline party rows.
- Header: 12px semibold, muted, left aligned by default.
- Amounts and quantities: right aligned, tabular numerals.
- Names / descriptions: left aligned.
- Status: compact text + semantic badge.
- Row hover: subtle gray; selected row: pale brand background.
- Use sticky headers for long lists and preserve filters during pagination.
- Provide sort indicators, column chooser, density control and CSV/XLSX export when appropriate.
- Bulk actions appear only after selection.
- Do not hide critical data behind hover-only actions.
- Mobile: transform rows into summary cards or use a deliberate horizontal-scroll region with pinned identifier; do not squeeze 8–12 columns into a narrow viewport.

### 5.4 Status badges

Use text labels, never color alone.

- **Paid / Active / Synced / In stock:** green.
- **Partially paid / Pending / Draft / Sync queued:** amber or neutral.
- **Overdue / Failed / Rejected / Out of stock:** red.
- **Sent / Processing / In transit:** blue.
- **Cancelled / Archived / Inactive:** neutral gray.

Badge padding 4px 8px, 12px semibold text, radius 6px. Status labels must reflect actual system state.

### 5.5 Cards and metric panels

- Cards should group related information, not act as decoration.
- Dashboard metric cards: label, figure, comparison period and small trend.
- Keep one primary metric per card.
- Trend indicators include text or accessible labels, not only arrows.
- Avoid more than 4 KPI cards in a row.
- Use dividers to group details within a panel instead of nesting cards inside cards.

### 5.6 Dialogs, drawers and confirmations

- Use dialogs for short decisions and confirmations.
- Use drawers for contextual details, filters and quick edit forms.
- Use full-page workflows for complex invoices, accounting entries and setup.
- Destructive confirmation must state what is affected and whether the action can be undone.
- For financial records, prefer cancel/void/credit-note workflows over hard deletion once posted.
- Escape closes non-destructive overlays; focus is trapped and restored on close.
- Clicking the backdrop should not accidentally discard unsaved work.

### 5.7 Toasts and alerts

- Toast for brief feedback: “Invoice saved as draft.”
- Inline alert for actionable or persistent issue: failed sync, GST validation failure, missing setup.
- Never use a toast as the only place for a critical error.
- Provide “View details” / “Retry” where possible.
- Success messages should not claim a remote operation succeeded when it is only queued locally.

### 5.8 Search, filters and command menu

- Global search opens with `Ctrl/⌘ K`.
- Search results include type, identifier, date and key status.
- Filter chips show active filters and have a one-click clear action.
- Provide date presets: Today, Yesterday, This week, This month, Financial year, Custom.
- Persist filters per page where sensible.
- Empty search results offer correction suggestions and clear filters.

### 5.9 Charts and data visualization

- Use charts to answer a specific business question, not as filler.
- Prefer bar charts for comparisons, line charts for trends and stacked bars for composition.
- Always label axes, periods, currency and units.
- Include a table or accessible summary for critical chart data.
- Do not use red/green alone to encode positive and negative values.
- Keep charts simple; no 3D charts, gradients or excessive legends.

---

## 6. Screen specifications

## 6.1 Authentication

### Sign in
- Centered form on a calm, light canvas with a restrained dark brand panel or abstract ledger illustration.
- Fields: email/phone, password, show password, remember device where appropriate.
- Actions: Sign in, Forgot password, Create account.
- Optional SSO only if implemented.
- Show password requirements and clear errors.
- Never expose whether an account exists unnecessarily in password recovery.

### Registration
- Keep initial account creation short: name, email/phone, password, consent to terms/privacy.
- Business details are collected in onboarding rather than crammed into registration.
- Verify email/phone as needed; allow recovery and resend.
- Include privacy and security links.

### Password reset / verification
- Single-purpose screen, clear instructions, resend timer if applicable.
- Success and failure states are explicit.
- Do not show sensitive tokens in URLs beyond necessary secure reset mechanics.

---

## 6.2 First-run onboarding and business setup

Use a stepper with a clear progress indicator and save-and-resume support.

1. **Business profile:** legal/trade name, business type, address, state, country, contact details.
2. **Tax setup:** GST registration status, GSTIN, state code, PAN where applicable, tax defaults.
3. **Financial preferences:** financial year, invoice numbering, default currency, rounding.
4. **Starting data:** add products/customers now or import later.
5. **Print setup:** choose invoice template and paper size; printer setup may be skipped.
6. **Team:** invite staff or skip.
7. **Review:** confirm configuration before entering the app.

Rules:
- Explain why each required field is needed.
- Validate GSTIN format and state relationship, but clearly distinguish format validation from authoritative verification.
- Never infer tax registration from a business name.
- Save draft progress automatically.
- Show setup checklist on dashboard until completed.
- Provide a “Configure later” route for non-blocking settings.

---

## 6.3 Dashboard / Overview

### Page objective
Answer: “How is my business doing, what needs attention, and what should I do next?”

### Layout
- Header: “Good morning” is optional; business date and financial period must be visible.
- Quick actions: New sale, New purchase, Add expense, Record payment.
- KPI row (configurable):
  - Sales today
  - Amount received
  - Outstanding receivables
  - Purchase / expenses
- Main row:
  - Sales trend with period selector
  - Cash / bank snapshot
- Secondary row:
  - Receivables aging
  - Low-stock alerts
  - Recent transactions
  - Pending tasks / sync queue
- Optional business health checklist for new accounts.

### Interactions
- KPI click opens the matching filtered report.
- Date-range changes update all linked metrics consistently.
- “Low stock” opens a filtered inventory list.
- Recent transactions allow invoice / payment detail access subject to permissions.
- Show last updated timestamp when data may be stale.

### States
- New business: setup checklist and primary action, not empty charts with zero data.
- Offline: banner showing local/offline status and pending sync count.
- Data loading: stable skeletons that match final layout.
- Partial failure: show which widget failed and allow retry without blanking the full page.

---

## 6.4 Sales invoices list

### Header
- Title: Sales invoices.
- Primary action: Create invoice.
- Secondary actions: Import, Export, Print selected (permission and state dependent).

### Filters
- Search by invoice number, party, phone, GSTIN.
- Date range, status, payment status, salesperson, tax type, amount range.
- Saved views may be added later.

### Table columns
Invoice no. | Date | Customer | Total | Paid | Balance | Status | Actions

- Invoice no. opens detail.
- Amounts use tabular numerals.
- Status and payment status are distinct.
- Overdue balance is explicit.
- Bulk selection only offers valid actions for selected records.

### Invoice detail
- Header with invoice number, status, party and total.
- Actions: Print, Download PDF, Share, Record payment, Create credit note, Duplicate as draft.
- Sections: line items, tax breakdown, payment history, notes, audit/activity.
- Posted financial data is not silently overwritten; edits follow defined accounting rules.

---

## 6.5 Create / edit sales invoice

### Layout
Use a two-column desktop layout:
- Main column: party, invoice metadata, item grid, notes.
- Summary column: tax breakdown, totals, payment state and save/issue controls.
- On mobile, stack sections and use a sticky bottom total/action bar.

### Sections
1. Document type: GST invoice, bill of supply, non-GST bill, quotation, proforma, delivery challan as appropriate.
2. Customer: searchable selector, add-new drawer, GSTIN and billing/shipping address.
3. Metadata: invoice number (system controlled), invoice date, due date, place of supply, reverse charge where applicable.
4. Items grid: product, description, HSN/SAC, quantity, unit, rate, discount, tax rate, amount.
5. Additional charges: freight, packaging, delivery, other configured charges.
6. Tax summary: taxable value, CGST, SGST, IGST, cess, discount and rounding.
7. Payment: cash/UPI/card/bank/credit/split payment, amount received, reference.
8. Notes and terms.
9. Final review and action.

### Calculation presentation
- Show subtotal, discount, taxable amount, tax components, additional charges, round-off and final total as separate rows.
- Make the final amount visually dominant but not oversized.
- Tax selection and calculation must be driven by validated business configuration and place-of-supply rules; the UI must not hardcode tax logic.
- Show a concise validation message if a tax configuration is incomplete.
- Make rounding transparent.

### Actions
- Save draft.
- Preview.
- Save / issue invoice.
- Save and print (only after a successful save/issue state).
- Cancel / discard with unsaved-change protection.

### Validation
- Required customer/document fields.
- Positive quantity and valid price.
- Tax rate and HSN/SAC validation where required.
- Customer GST details when required by document rules.
- Prevent accidental duplicate submissions.
- Clearly explain why an action is blocked.

---

## 6.6 POS / fast checkout

### Design priority
Speed, legibility and low cognitive load. POS is a dedicated workspace, not a generic invoice form.

### Desktop layout
- Top bar: business / outlet, online-offline state, cashier, date, shortcut help.
- Left / center: search and barcode input, category filters, product grid/list.
- Right panel: cart, customer, discount, tax-inclusive/exclusive details, payment.
- Bottom / footer: item count, total, hold sale, clear cart, checkout.

### Product tile
Name, optional thumbnail, SKU/barcode, available quantity, selling price. Low-stock / out-of-stock states are explicit. Do not display purchase cost to cashier roles unless permitted.

### Cart
- Editable quantity and unit.
- Remove item with undo where safe.
- Per-line discount only when permission allows.
- Clear subtotal, discount, tax and total.
- Keyboard navigation and barcode scanner support.
- Prevent overselling unless an authorized policy permits it.

### Checkout flow
1. Confirm cart and customer (walk-in supported if configured).
2. Select payment method.
3. For split payments, show remaining balance live.
4. For credit sale, show customer outstanding / credit limit warning.
5. Confirm transaction.
6. Show receipt success with print, PDF/share, new sale.
7. If offline, label the transaction “Saved on this device — sync pending” rather than “Synced”.

### Suggested keyboard shortcuts
- `/` or `Ctrl/⌘ K`: focus product search.
- `F2`: select customer (configurable).
- `F4`: payment.
- `F8`: hold sale.
- `Esc`: close non-destructive overlay.
- `Enter`: confirm focused safe action.
- Shortcuts must be discoverable, remappable where needed and not conflict with browser or assistive technology behavior.

### Mobile POS
- Search-first product selection.
- Cart as a full-screen sheet.
- Persistent checkout bar.
- Touch targets at least 44px.
- Do not require camera scanning if manual search or external scanner is available.

---

## 6.7 Purchases and supplier bills

- List columns: bill no., supplier, date, due date, total, paid, balance, status.
- Purchase form mirrors invoice patterns to reduce learning cost.
- Support supplier bill number separately from internal document number.
- Items increase stock only according to transaction state and configured workflow.
- Purchase returns and debit notes link to original purchase where possible.
- Show payable balance and payment history.
- Duplicate supplier bill warnings should be non-blocking until user reviews the match.

---

## 6.8 Products and inventory

### Product list
- Search by product name, SKU, barcode, HSN/SAC.
- Filters: category, brand, stock state, warehouse, tax rate, active/inactive.
- Columns: product, SKU, category, selling price, available stock, unit, tax, status.
- Primary action: Add product; secondary: Import, Generate barcode, Export.

### Product create/edit
- Identity: name, SKU, barcode, category, brand.
- Tax: HSN/SAC, GST rate, tax-inclusive/exclusive selling price.
- Pricing: purchase cost, selling price, MRP, wholesale price, minimum price (permission gated).
- Units: primary / secondary units and conversions.
- Stock: opening stock, reorder level, warehouse, batch/serial tracking.
- Optional fields: images, description, supplier, variants.
- Purchase cost and margin data must be permission protected.

### Stock movement ledger
Columns: date, movement type, reference, warehouse, quantity in, quantity out, running balance, user.
- Each movement links to source transaction.
- Corrections are adjustments with reason and audit trail, not silent edits to historical stock.
- Show stock freshness / sync status where offline operations can affect current figures.

### Warehouses and transfers
- Warehouse selector and location-specific stock.
- Transfer workflow: source, destination, items, quantities, transit / received state.
- Show in-transit quantity separately.
- Reject invalid same-source/destination transfer.
- Confirm receipt and reconcile discrepancies with an adjustment record.

### Batches / expiry
- Batch number, manufacture date, expiry date, available quantity.
- Configurable alerts before expiry.
- List filters for expired, expiring soon, and healthy stock.
- Never sell expired stock silently; enforce configured policy and show clear reason.

### Serial / IMEI
- Unique serial / IMEI association to product and transaction.
- Warranty dates and customer association where relevant.
- Validate duplicates and provide a traceable history.

### Barcode and labels
- Barcode generation: supported symbologies such as EAN-13, Code 128 and QR where suitable.
- Label designer: paper size, grid, margins, product fields, price and barcode.
- Preview before print.
- Camera, USB and Bluetooth scanner flows must provide manual fallback.
- Do not promise scanner compatibility without testing the target hardware.

---

## 6.9 Customers, suppliers and party ledger

### Party list
- Tabs: Customers / Suppliers / All parties (if supported).
- Columns: name, phone, GSTIN, outstanding, credit status, last activity.
- Search by name, phone, GSTIN and ledger reference.
- Add party via focused drawer or page.

### Party profile
- Header with name, contact, GSTIN and outstanding.
- Quick actions: New invoice, Receive payment, Share ledger, Edit.
- Tabs: Overview, Transactions, Ledger, Addresses, Notes.
- Show total receivable/payable, overdue amount and last payment.
- Credit limit warnings must be actionable and permission aware.

### Ledger sharing
- Show exactly what information will be shared and with whom.
- Use expiring, revocable links where supported.
- Avoid exposing unrelated business data.
- Link view should be read-only and clearly branded.
- Show last updated time and allow authorized download.

---

## 6.10 Payments, cash and bank

### Payments list
- Filters: received/paid, method, account, date, status, reference.
- Columns: date, party, reference, method, amount, allocation status.
- Detail shows linked invoices/bills, amount allocated, unallocated balance and audit history.

### Record payment
- Party, direction (in/out), date, method, account, amount, reference.
- Invoice allocation table with due amounts.
- Split allocation and partial payment support.
- Overpayment handling must be explicit; do not silently discard remaining amount.
- Receipt / payment voucher preview before finalizing if appropriate.

### Cash and bank
- Account balances, transactions, transfers, opening balances and reconciliation.
- Reconciliation UI pairs bank statement lines with ledger entries.
- Matched / suggested / unmatched states are distinct.
- Reconciliation suggestions must be reviewable and reversible according to accounting rules.

---

## 6.11 Accounting

### Accounting dashboard
- Period selector and links to P&L, balance sheet, trial balance, cash flow and daybook.
- Show unposted entries, reconciliation exceptions and period-close warnings.
- Keep accounting reports grounded in the accounting ledger, not independently recomputed dashboard-only values.

### Chart of accounts
- Tree/table view: code, account name, type, parent, opening balance, current balance, status.
- Prevent invalid parent/child structures and inappropriate account-type changes.
- Clearly indicate system accounts that cannot be deleted.

### Journal entry
- Date, voucher number, narration, account rows, debit, credit, attachment.
- Running totals show total debit and credit.
- Do not allow posting unless balanced and all required fields are valid.
- Draft vs posted state is obvious.
- Posted entries require a defined correction/reversal workflow.

### Ledger / trial balance / daybook
- Strong period filter, account filter and export.
- Running balance where applicable.
- Opening balance, debit, credit and closing balance are visually distinct.
- Exported figures must match the on-screen filters and period.

### Financial statements
- Profit & loss, balance sheet and cash flow.
- Include reporting period, business, currency and “as of” date.
- Provide drill-down from summary line to source ledger entries.
- Show notes for incomplete data or unreconciled sources.
- Financial reports should not use decorative visualizations that obscure accounting structure.

---

## 6.12 GST and compliance

### GST overview
- Business GST profile and registration state.
- Compliance checklist / return period selector.
- Filing preparation status and pending exceptions.
- Clearly distinguish “Prepared”, “Validated”, “Exported”, “Filed” and “Failed”.
- Never imply a return was filed merely because a JSON file was generated.

### GSTR-1 / GSTR-3B / GSTR-2B reconciliation
- Period selector and summary totals.
- Tables grouped by appropriate transaction / document category.
- Validation errors with severity, affected record and suggested correction.
- Reconciliation states: matched, mismatch, missing in books, missing in statement, ignored with reason.
- Provide export and error report.
- Keep the original imported statement and reconciliation history traceable.

### E-invoice / IRN
- Invoice eligibility and validation state.
- Generate / cancel actions only where supported and authorized.
- IRN, acknowledgement number/date and QR details displayed after confirmed response.
- Handle timeout as “Status unknown — check before retrying” if duplicate generation is possible.
- Retry logic must avoid duplicate external submissions.

### E-way bill
- Part A / Part B, transporter, vehicle, distance and validity information as applicable.
- Clear errors from external API.
- Status history, expiry and cancellation state.
- Never present mock / demo API responses as live compliance data.

### GST UI guardrails
- Tax logic must be validated by qualified GST domain review before production.
- Separate format validation from authoritative verification.
- Label API status and last checked time.
- Show provider outage and manual export fallback.
- Preserve request / response identifiers and audit history while redacting secrets.

---

## 6.13 Reports and analytics

### Report library
Organize by Sales, Purchases, Inventory, Receivables/Payables, Tax and Accounting.

Each report includes:
- Title, purpose and reporting period.
- Business / branch / warehouse scope.
- Filters and visible active-filter chips.
- Summary totals, table and export.
- Last updated timestamp where relevant.
- Empty state explaining how data enters the report.

### Receivables / payables aging
Buckets: 0–30, 31–60, 61–90, 90+ days, configurable to business policy.
- Show total outstanding and overdue totals.
- Drill down to party and invoice.
- Avoid suggesting aging is a legal due-date determination; use configured due-date logic.

### Export
- Format choices: CSV / XLSX / PDF as supported.
- Preview selected columns and date range.
- Export should respect role permissions and tenant scope.
- Large exports show progress and provide a secure download when ready.

---

## 6.14 AI bookkeeping and import review

### Import flow
1. Upload PDF / CSV / XLSX / bank statement.
2. Show detected format and source period.
3. Preview parsed rows and mapping.
4. Display extraction confidence and uncertain fields.
5. Suggest categories / ledger matches.
6. User reviews and approves selected entries.
7. Commit entries and show a summary with rejected rows and errors.

### Review queue
- Separate “Suggested” from “Approved / Posted”.
- Each suggestion explains why it was proposed and links to source evidence.
- Confidence is supporting context, not proof.
- Actions: Approve, Edit, Reject, Open source.
- Bulk approval is available only for low-risk, clearly matched cases and remains auditable.
- AI must not silently post irreversible accounting changes, alter tax records or reconcile a bank statement without an authorized approval flow.

### AI states
- Processing, needs review, ready, partial extraction, failed.
- Preserve original file and row-level provenance according to retention policy.
- Clearly identify generated suggestions vs verified facts.
- Provide undo/reversal workflow for committed actions where accounting rules permit.

---

## 6.15 CA portal and team management

### Team members
- Member, role, assigned businesses, invitation status, last active.
- Invite / resend / revoke.
- Show role description before assigning.
- Warn when permission changes broaden access to financial or customer data.

### Roles and permissions
Permissions are explicit by resource and action: view, create, edit, delete/void, export, approve, print, view purchase cost, override price, manage users.
- Default to least privilege.
- Do not rely only on hidden UI; enforce permissions on the server.
- Disabled actions should explain required permission when appropriate.

### CA workspace
- Client/business switcher.
- Assigned clients only.
- GST and accounting reports, ledger exports, reconciliation, audit log.
- Show access scope and invitation status.
- Client access can be revoked and logged.
- Avoid cross-client data in search results or recent activity.

---

## 6.16 Online store and order management

### Store setup
- Store name, slug, theme, contact, delivery settings, catalog visibility.
- Custom domain only when supported and verified.
- Product selection and inventory sync settings.
- Preview desktop/mobile before publishing.

### Storefront
- Fast catalog, categories, search, product details and availability.
- Clear order / quotation action.
- Do not expose internal cost, margin, supplier or warehouse notes.
- Stock status must reflect the store's configured source and sync freshness.

### Orders
- New, accepted, processing, dispatched, completed, cancelled.
- Link order to customer and later invoice.
- Avoid decrementing stock twice when converting an order to a sale.
- Show sync errors and retry action.

---

## 6.17 Marketing, WhatsApp/SMS and loyalty

### Campaign list
- Campaign name, audience, channel, schedule, delivery status, cost/credits if applicable.
- Compose screen: audience, message template, preview, compliance checks, schedule/confirm.
- Show recipient count before sending.
- Provide opt-out / consent handling according to applicable requirements.
- Avoid misleading “delivered” states when only accepted by provider.

### Loyalty
- Customer points balance and transaction ledger.
- Earning/redemption rules visible before applying.
- POS redemption displays resulting amount and points remaining.
- Manual adjustments require reason and audit record.
- Do not let negative balances occur unless a specific approved policy supports them.

---

## 6.18 Subscription and billing

- Plan comparison: Lite, Plus, Pro, Max; clearly state feature limits and billing cadence.
- Trial banner should show actual trial end date and available actions.
- Current plan, usage, renewal date, invoices, payment method and status.
- Upgrade / downgrade / cancel flows explain effective date and consequences.
- Failed payment has a recovery path without destructive data loss.
- Refund / money-back policy text must match actual business terms.
- Never show a successful subscription state until verified server-side / provider-side.

---

## 6.19 Public tools and marketing website

The public marketing website is separate from the authenticated application shell.

### Landing page
- Hero: clear promise for Indian small businesses, not unsupported numerical claims.
- Product UI preview.
- Features grouped by Billing, Inventory, Accounting, GST and Offline/POS.
- “How it works”, supported workflows, pricing, FAQs and final CTA.
- Trust claims must be substantiated; do not invent customer logos or testimonials.

### Public utility tools
- GST invoice generator, GST calculator, late fee / interest calculator, EMI calculator, margin / markup calculator, HSN/SAC directory, barcode generator.
- Give each tool a focused page, visible inputs, clear results and explanation of assumptions.
- Tax calculations should include a disclaimer that outputs are estimates and require review for the user's situation.
- Avoid forced sign-up before basic free tool use unless the product requirements explicitly require it.
- SEO pages need accessible content, canonical metadata, sitemap, structured data where appropriate and fast rendering.

---

## 6.20 Import, migration and integrations

- Import wizard: file upload, type detection, column mapping, preview, validation, duplicate resolution, commit.
- Show row counts: ready, warning, error, skipped.
- Provide downloadable error report.
- Never partially commit data without showing what succeeded and what failed.
- Tally import/export: choose format / version, map fields, validate, preview, export and show validation errors.
- Integration settings: connection status, permissions, last sync, errors, disconnect.
- Secrets and API credentials are never displayed in full after saving.

---

## 6.21 Audit log, notifications and help

### Audit log
Columns: time, actor, action, entity, business, source/device, result.
- Filters by actor, action, resource and date.
- Details show before/after values only for authorized viewers.
- Audit logs should be append-only from the application's perspective and protected against ordinary user edits.

### Notifications
- Group by unread / all, type and date.
- Each notification links to the relevant record.
- Mark read / mark all read.
- Settings control channels where supported.
- Critical sync or compliance errors remain accessible until resolved or acknowledged.

### Help
- Contextual help link on complex workflows.
- Searchable documentation and troubleshooting.
- Show product version and support request ID when reporting a problem.
- Do not show fake live chat availability.

---

## 7. Responsive behavior

### Desktop (1024px and above)
- Full sidebar by default.
- Multi-column forms and summary panels.
- Dense tables with sticky headers.
- Keyboard shortcuts supported.

### Tablet (768–1023px)
- Sidebar collapses to icon rail or drawer.
- Reduce dashboard grid to two columns.
- Long forms use two columns only where labels and controls remain clear.
- Tables may scroll horizontally with pinned first column.

### Mobile (320–767px)
- Navigation uses a drawer; current business and sync state remain reachable.
- Single-column content; stack form fields.
- Primary action remains easy to reach.
- Tables become summary cards or intentional scroll containers.
- POS uses a touch-first full-screen cart and checkout.
- Avoid hover-only controls.
- Touch targets minimum 44×44px where practical.
- Sticky bottom bars must respect safe areas and not cover validation messages.

### Small-screen priorities
1. Current business and sync status.
2. Page title and primary action.
3. Critical total / balance / status.
4. Main task controls.
5. Secondary metadata.

---

## 8. Accessibility requirements

Target **WCAG 2.2 AA** as the design and implementation goal.

- Text contrast at least 4.5:1 for normal text and 3:1 for large text; meaningful controls and boundaries must also be distinguishable.
- Full keyboard operation with logical tab order and visible focus.
- No color-only status; include text and/or icon.
- Inputs have programmatic labels and accessible error messages.
- Dialogs announce titles and manage focus correctly.
- Charts have text summaries / table alternatives.
- Respect `prefers-reduced-motion`.
- Avoid flashing and unnecessary animated transitions.
- Use semantic landmarks, heading hierarchy and accessible names for icon-only controls.
- Screen-reader announcements for save, sync, payment and validation outcomes.
- Support zoom to 200% without loss of core functionality.
- Error messages state what happened and how to fix it.
- Never move focus unexpectedly after background sync.

---

## 9. Motion and interaction feedback

- Standard transitions: 120–180ms for hover/focus/press; 180–260ms for drawers and dialogs.
- Use motion to show state change, not as decoration.
- Avoid springy, bouncy animations in accounting workflows.
- Table row selection and status changes should be immediate.
- Skeletons only when loading is likely to last long enough to be noticed; prefer stable placeholders over layout shift.
- On successful save, show confirmation and preserve context.
- On failure, preserve user input and expose a retry or correction path.
- Respect reduced motion by removing nonessential transitions.

---

## 10. Offline-first and sync UX

Offline support is a first-class product behavior and must be explicit.

### Global sync indicator
States:
- **Online / Synced:** current device has no pending changes.
- **Offline:** network unavailable; local features may remain available.
- **Pending sync:** changes are queued locally.
- **Syncing:** data transfer in progress.
- **Sync issue:** one or more records require attention.
- **Conflict:** user decision or defined resolution is required.

Use text labels in addition to icons. Clicking the indicator opens a sync panel with pending count, last successful sync, recent failures and safe retry.

### Offline transactions
- Show a persistent but non-blocking offline banner.
- Clearly label local-only receipts and transactions.
- Use a local transaction identifier until server confirmation.
- Do not display “Synced” or “Filed” before confirmation.
- Prevent duplicate invoice creation on retry using idempotent identifiers.
- When a record is pending, show which actions remain unavailable.

### Conflict resolution
- Present local version and server version with changed fields.
- Explain which choice affects inventory, accounting or tax records.
- Never auto-merge conflicting financial amounts silently.
- Provide safe retry / support path and audit resolution.

---

## 11. Empty, loading, error and success states

Every major page must design these states before production.

### Empty state
- Briefly explain what belongs here.
- Offer one relevant primary action.
- Optional sample data only in demo mode and clearly labelled.

### Loading state
- Skeletons match expected final layout.
- Do not show fake zero totals while loading.
- Preserve current filters and layout.

### Error state
- Plain-language summary, actionable next step, retry where safe.
- Include a reference ID for support when useful.
- Preserve user input and avoid leaking technical stack traces.

### Permission state
- Explain that access is restricted and identify the appropriate admin action.
- Do not reveal inaccessible customer / financial details.

### Success state
- Confirm what happened and whether it is saved locally, synced, issued, printed or filed.
- Offer next likely action.
- Use distinct states for “saved draft”, “issued”, “payment recorded” and “sync complete”.

---

## 12. Financial safety and destructive action rules

- Posted transactions should not be silently edited or hard-deleted.
- Use void, reversal, credit note, debit note or adjustment flows where appropriate to accounting and tax rules.
- Confirm destructive actions with record names and impact.
- Require reason for stock adjustments, price overrides and manual ledger changes where configured.
- Apply permission checks on the server as well as in the UI.
- Display source transaction links for stock and accounting movements.
- AI-generated suggestions require human review before high-impact posting.
- Payment status must be based on verified transaction records, not client-only state.
- GST filing and e-invoice states must be based on confirmed provider/API responses.
- Avoid optimistic UI for irreversible financial state changes; use a pending state until confirmed.

---

## 13. Suggested implementation architecture

The visual system is framework-agnostic. Recommended implementation for the existing project direction:

- **Framework:** Next.js + React + TypeScript.
- **Styling:** Tailwind CSS using CSS custom properties above.
- **Components:** shadcn/ui or equivalent accessible primitives, customized to this system.
- **Icons:** Lucide, consistent 18px default stroke icons.
- **Forms:** React Hook Form + schema validation (e.g. Zod) if suitable for the stack.
- **Tables:** TanStack Table or equivalent, with server-side filtering/pagination for large datasets.
- **Charts:** Recharts or equivalent accessible charting solution.
- **PWA/offline:** service worker + IndexedDB; Dexie or another maintained local persistence layer.
- **Server state:** query/cache layer with explicit invalidation and sync semantics.
- **Print:** dedicated print templates and tested page-size presets.
- **Testing:** component tests, accessibility checks, responsive tests and end-to-end workflow coverage.

Do not place GST calculations, accounting rules, authorization or tenant-isolation logic solely in client code.

### Suggested component folder organization

```text
src/
  app/
    (auth)/
    (app)/
      dashboard/
      sales/
      purchases/
      pos/
      inventory/
      parties/
      payments/
      accounting/
      gst/
      reports/
      ai-bookkeeping/
      team/
      settings/
  components/
    app-shell/
    navigation/
    data-display/
    forms/
    feedback/
    overlays/
    charts/
    billing/
    inventory/
    accounting/
    gst/
  design-system/
    tokens.css
    typography.css
    globals.css
  lib/
    permissions/
    formatting/
    validation/
    sync/
  tests/
```

This is a suggested organization, not a required exact route structure.

---

## 14. Formatting conventions

- Currency defaults to INR (`₹`) when the business currency is INR; use locale-aware formatting and store currency explicitly.
- Amounts: consistent decimal precision based on currency and accounting rules.
- Dates: use the business locale and timezone; provide unambiguous date labels in exports.
- Store timestamps in a consistent canonical format and render in the relevant business timezone.
- Negative amounts: use a minus sign and descriptive labels; do not rely on red alone.
- Invoice numbers, GSTIN, HSN/SAC, SKU, IRN and payment references must be copyable.
- Distinguish internal record ID from customer-facing document number.
- Never hardcode example totals in production UI.
- For empty values, use an em dash or explicit “Not provided”; avoid a mix of `0`, blank and `N/A` without semantic meaning.

---

## 15. Invoice and print design system

Print output is a distinct surface, not a screenshot of the app.

### Supported layouts
- A4 and A5 invoice.
- 58mm and 80mm thermal receipt.
- Barcode / product labels.
- Bulk print queue and multi-document PDF export.

### Print rules
- White background, black primary text, high contrast.
- Keep totals and tax breakdown legible.
- Avoid backgrounds that consume ink.
- Respect printer margins and page breaks.
- Prevent item rows from splitting awkwardly across pages.
- Keep business legal details, GSTIN, invoice metadata and tax summary in predictable positions.
- QR / IRN content must be generated from validated source data.
- Preview at actual target page size.
- Provide separate template previews for A4/A5 and thermal widths.
- Test with real supported printers before claiming compatibility.

### Template themes
- Modern: clean indigo highlights, balanced spacing.
- Minimal: monochrome, compact and printer-friendly.
- Retail / Compact: optimized for frequent item lines and thermal output.
- Premium: restrained typography and whitespace, no decorative elements that reduce legibility.
- Custom: logo, business details, selected fields and permitted color choices.

---

## 16. Content and microcopy guide

Use direct, specific language.

**Prefer**
- “Save draft”
- “Issue invoice”
- “Record payment”
- “3 invoices need attention”
- “Saved on this device · Sync pending”
- “Couldn’t verify GSTIN. Check the number or try again.”
- “This entry is posted. Create a reversal to correct it.”

**Avoid**
- “Oopsie!”
- “Something went wrong” without a next step.
- “Success!” without saying what succeeded.
- “100% GST compliant” unless independently substantiated and legally approved.
- “AI handled everything” for workflows requiring review.

Button labels should describe the action and its consequence. Confirmation dialogs should avoid vague “Are you sure?” copy.

---

## 17. UX quality checklist

Before approving each screen, verify:

### Visual hierarchy
- [ ] The page purpose is clear within five seconds.
- [ ] There is one dominant primary action per region.
- [ ] Financial amounts and statuses are easy to scan.
- [ ] Spacing and typography follow tokens.
- [ ] Accent color is used intentionally.

### Workflow
- [ ] Primary task can be completed without unnecessary navigation.
- [ ] Required fields and tax calculations are clear.
- [ ] Save / issue / post / file states are distinct.
- [ ] Back navigation does not lose work unexpectedly.
- [ ] Destructive or irreversible actions are guarded.

### Data and finance
- [ ] Amounts use tabular numerals and correct locale.
- [ ] Table columns have appropriate alignment.
- [ ] Totals and tax breakdown reconcile.
- [ ] Permissions are respected in UI and API.
- [ ] Audit history and source records are accessible.

### Accessibility and responsive behavior
- [ ] Keyboard-only path works.
- [ ] Focus is visible.
- [ ] Contrast and status labels are accessible.
- [ ] Mobile touch targets are large enough.
- [ ] No horizontal page overflow at 320px.
- [ ] Tables and forms have a deliberate mobile strategy.
- [ ] Reduced motion is respected.

### Offline and errors
- [ ] Online/offline/sync status is visible.
- [ ] Local-only changes are not misrepresented as synced.
- [ ] Retry behavior is safe and idempotent.
- [ ] Failed actions preserve user input.
- [ ] Conflicts are visible and resolvable.

---

## 18. UX critique: common risks to avoid

1. **Dashboard overload:** do not put every metric and module on the home page. Prioritize four KPIs, recent activity and actionable exceptions.
2. **Generic card spam:** not every table, filter or form needs its own card. Use clear sections and dividers.
3. **POS designed like an admin panel:** checkout must prioritize product search, cart and payment.
4. **Invoice form with no live summary:** keep totals and tax breakdown visible as the user edits.
5. **Ambiguous sync states:** pending local changes must never look fully synced.
6. **Status by color only:** every state needs a text label and accessible meaning.
7. **Hidden critical actions:** do not hide print, payment or validation actions behind hover-only menus.
8. **Overly dense tables on mobile:** use summary cards or controlled horizontal scroll.
9. **Dangerous optimism:** don't show “paid”, “filed”, “issued” or “synced” before authoritative confirmation.
10. **Tax logic in presentation code:** UI displays validated results; business logic belongs in tested domain/server layers.
11. **AI automation without review:** financial suggestions need source evidence and approval controls.
12. **Fake trust signals:** no invented testimonials, compliance badges, customer logos or performance claims.

---

## 19. Recommended build order for design and implementation

### Phase 1 — Design foundations
- Tokens, typography, icon rules, buttons, inputs, badges, tables, dialogs, toasts.
- App shell, navigation, business switcher, global search and sync status.
- Accessibility and responsive foundations.

### Phase 2 — Core business flows
- Authentication and onboarding.
- Dashboard.
- Customers / suppliers.
- Products and stock.
- Sales invoice list, create, detail, PDF/print.
- Purchase bills.
- Payments and basic ledger.

### Phase 3 — High-frequency operations
- POS.
- Barcode and label printing.
- Stock movements and warehouses.
- Returns / credit notes.
- Core financial and inventory reports.

### Phase 4 — Compliance and collaboration
- GST overview and return preparation.
- E-invoice / e-way bill states.
- Roles, CA portal and audit logs.
- Import and migration.

### Phase 5 — Advanced modules
- Offline sync and conflict resolution.
- AI bookkeeping review.
- Online store, marketing, loyalty.
- Subscription management.
- Desktop/mobile companion surfaces.

Build the visual system and core transaction flows before investing in decorative landing-page polish.

---

## 20. Definition of design-ready

A feature is design-ready when:
- Its primary user and goal are defined.
- The main path and error paths are mapped.
- Loading, empty, offline, permission and success states are specified.
- Responsive behavior is documented.
- Relevant permissions and financial safety constraints are defined.
- Data labels and terminology are agreed.
- Components use the tokens in this document.
- Accessibility checks are included in acceptance criteria.
- It has been reviewed against the UX quality checklist.

## Final direction

Youthinity Book should combine the quiet precision of modern productivity software with the legibility and explicitness required by billing and accounting. Use a dark, stable navigation shell to anchor the product and a light, high-contrast workspace for daily work. Keep indigo as a focused action color; let tables, forms, totals, status labels and clear workflows do the heavy lifting.

**Design principle to protect above all:** users must always understand what a financial action will do, what state it is in, and whether the result is saved locally, synced, posted, paid or officially submitted.
