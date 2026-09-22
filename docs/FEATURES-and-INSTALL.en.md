# Pinova — Features & Installation Guide

> This document summarizes the features and installation steps of **Pinova**, a fully automated e-pin / digital goods selling script.
> Live demo: **[pinova.epinsoft.com.tr](https://pinova.epinsoft.com.tr)** · Purchase: **pazarlama@epinsoft.com.tr**

---

## 1. Product Overview

**Pinova** is a ready-to-sell **e-pin selling software** (PHP) built to sell game e-pins, game codes, gift cards, in-game currency and any kind of **digital product with automatic delivery**.

The moment a customer completes payment, the stock code is delivered **automatically within seconds** — no manual work required. It is a **single-vendor** shop model (your own store) managed from a single admin panel.

**Who it's for:** Entrepreneurs, resellers and digital-goods sellers who want to launch their own e-pin / digital product store.

**Example use cases:** Steam keys, PUBG UC, Valorant VP, Minecraft, PlayStation codes, gift cards, in-game currency and similar instant-delivery digital products.

---

## 2. Features

### 2.1 Automatic Delivery & Stock
| Feature | Description |
|---|---|
| Instant automatic delivery | The stock code is delivered to the customer automatically the moment payment is confirmed. |
| AES-encrypted stock | Stock codes are stored **encrypted** in the database, reducing leak risk. |
| Stock management | Per-product stock pool; automatic "out of stock" when depleted. |
| Order & invoice records | Every sale is logged; the delivered code is traceable. |

### 2.2 Wallet & Payments
| Feature | Description |
|---|---|
| Wallet (balance) system | Customers can top up a balance and pay from it. |
| Multiple payment gateways | Several payment providers supported (see 4.6 — connect your own POS). |
| Balance top-up flow | Secure balance top-up via the payment gateway. |

### 2.3 Reseller System
| Feature | Description |
|---|---|
| Dealer pricing | Special discounted prices can be defined for resellers. |
| Dealer panel | A dedicated management/order view for resellers. |

### 2.4 Content & Marketing
| Feature | Description |
|---|---|
| AI blog automation | SEO-focused blog content generation with OpenAI / Gemini / Claude. |
| SEO-friendly | Search-engine-friendly URL structure and content foundation. |
| Mobile-friendly | Responsive interface. |

### 2.5 Admin Panel
| Feature | Description |
|---|---|
| Product / category management | Manage products, categories, prices and images. |
| Stock management | Bulk stock upload; encrypted code pool. |
| Orders & reports | Sales list, revenue reports, customer records. |
| Comprehensive control | Dozens of admin pages covering every aspect of the store. |

---

## 3. Technical Architecture

| Layer | Technology |
|---|---|
| Backend | PHP (CodeIgniter-based MVC) |
| Database | MySQL / MariaDB |
| Frontend | Responsive HTML/CSS/JS |
| Scheduled jobs | Cron (blog generation, etc.) |
| Deployment | Shared hosting / VPS; Cloudflare-compatible |
| Recommended PHP | 7.4+ (latest version recommended) |

---

## 4. Installation & Configuration

> The steps below are a general installation flow. Actual credentials (DB password, admin login, keys) are provided separately during setup; they are not included in this document.

### 4.1 Requirements
- PHP 7.4+ (recommended), MySQL/MariaDB
- Apache/LiteSpeed (`.htaccess` / URL rewrite support)
- SSL certificate (HTTPS) — recommended for production

### 4.2 Uploading the Files
```
# Upload the source to your web root (FTP/SFTP or file manager)
# e.g. public_html/ or your domain root
```

### 4.3 Importing the Database
```
# Import the schema via phpMyAdmin or CLI
mysql -u USER -p DATABASE < pinova.sql
```

### 4.4 Configuration
- **base_url** (`config.php`): your site's full address (e.g. `https://example.com/`).
- **Database** (`database.php`): host, user, password, database name.
- **Encryption key** (`config.php`): `$config['encryption_key']` — set a strong, unique value (stock codes are stored encrypted).

### 4.5 Cron Setup
```
# Scheduled jobs such as AI blog generation (example — every 30 minutes)
*/30 * * * * curl -s "https://example.com/cron/..." >/dev/null 2>&1
```

### 4.6 Payment Gateways (IMPORTANT — Selling Point)
Pinova ships payment gateways as **placeholders (empty credentials)**. This means:

- You connect **your own payment provider account** (iyzico, Stripe, PayTR, etc.) from the **admin panel**.
- Payments flow directly to **your** POS/account; no middleman.
- Easily adaptable to a different country/provider.

> In the demo environment the gateways have no credentials, so they run in **demo mode**; when going live you enter your own keys.

### 4.7 First Use
1. Log in to the admin panel (login details provided at delivery).
2. Add categories and products.
3. Upload stock (codes) to products — codes are stored encrypted.
4. Enter your payment gateway details.
5. Verify automatic delivery with a test order.

---

## 5. Delivery Package

- Full source code
- Database schema
- Installation support
- Features are summarized in this document; contact us for custom requests.

---

## 6. Contact

- 🌐 **Web:** [epinsoft.com.tr](https://epinsoft.com.tr)
- ✉️ **Email:** pazarlama@epinsoft.com.tr
- 📞 **Phone:** +90 850 255 18 01
- ▶ **Live demo:** [pinova.epinsoft.com.tr](https://pinova.epinsoft.com.tr)
