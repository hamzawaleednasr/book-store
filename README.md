# Django Digital Book Store

A production-oriented **digital book e-commerce system** built with Django, designed around real-world payment flows, clean separation of concerns, and an analytics-ready admin dashboard.

This project focuses on selling **digital products (PDF books)** with a complete checkout lifecycle, not a generic CRUD store.

---

## 🧠 Core Concept


The application is built around a **transaction-driven order lifecycle**:

Cart (Session) → Transaction → Payment (Stripe / PayPal) → Order → Email Confirmation

Orders are only created **after successful payment confirmation via webhooks**, ensuring data consistency and realistic business logic.

---

## 🚀 Key Features

### 🛍️ Digital Products
- Products represent **PDF books**
- Author & Category relationships
- Featured products for homepage curation
- No inventory complexity (intentional design)

### 🛒 Session-Based Cart
- Anonymous cart using Django Sessions
- JSON-based cart storage
- AJAX add/remove operations
- Automatic cleanup after checkout

### 💳 Payments
- **Stripe** (PaymentIntent + Webhooks)
- **PayPal** (IPN)
- Secure verification before order creation
- Payment metadata linked to internal transactions

### 📦 Orders & Transactions
- Clear separation between Transaction and Order
- Snapshot of customer data and purchased items
- OrderProduct model preserves historical pricing
- Read-only order management in admin

### 📊 Admin Reporting Dashboard
- Custom Django Admin view
- Yearly, monthly, and weekly revenue aggregation
- ORM-based analytics (no raw SQL)
- Designed for visualization and business insights

### 🌍 Internationalization
- Arabic-first configuration (`ar-sa`)
- Fully translatable views, forms, and admin labels
- Ready for multi-language expansion

---

## 🧩 Architecture Overview

``` text
django_store/
│
├── store/
│   ├── models.py        # Products, Categories, Authors, Cart, Orders
│   ├── views.py         # Storefront, product listing, cart operations
│   ├── urls.py          # Store routing
│   ├── admin.py         # Product & order admin configuration
│   └── templates/       # Storefront templates
│
├── checkout/
│   ├── models.py        # Transaction model
│   ├── views.py         # Stripe & PayPal payment flows
│   ├── webhooks.py      # Payment confirmation handlers
│   ├── forms.py         # User info & custom PayPal form
│   └── urls.py          # Checkout routing
│
├── reports/
│   ├── models.py        # Reporting models
│   ├── admin.py         # Custom admin analytics dashboard
│   └── templates/       # Admin report templates
│
├── templates/
│   └── base.html        # Global layout
│
├── static/              # CSS, JS, images
│
├── django_store/
│   ├── settings.py      # Project configuration
│   ├── urls.py          # Root URL configuration
│   └── wsgi.py / asgi.py
│
└── manage.py
```

--- 

## 🛠️ Tech Stack

- Python 3.10
- Django
- Stripe API
- PayPal IPN
- SQLite (local)
- WhiteNoise (static files)
- Django Admin (customized)

---

## ⚙️ Local Setup

```text
git clone https://github.com/hamzawaleednasr/book-store.git  
```
```text
python -m venv venv
```
```text
venv\Scripts\activate  
```
```text
pip install -r requirements.txt  
```
```text
python manage.py migrate  
python manage.py createsuperuser  
python manage.py runserver  
```
---

## 🔐 Security Notes

For production usage:
- Move secrets to environment variables
- Use DecimalField for monetary values
- Wrap payment and order creation in atomic transactions
- Add webhook idempotency checks

---

## 📌 Project Scope

This project intentionally avoids:
- User authentication complexity
- Inventory management
- Physical shipping logic

The focus is **clean payments, correct order lifecycle, and maintainable architecture**.

---

## 👤 Author

**Hamza Waleed**
