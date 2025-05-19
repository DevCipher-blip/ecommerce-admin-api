# E-commerce operations API

## Inventory and sales share a data model

Products, inventory records, inventory-change logs, and sales are separated into schema, model, CRUD, and router layers. The [entity diagram](ERD.png) is the quickest overview; follow a sale through [the sales CRUD module](app/crud/sales.py) to see how it affects stored state.

Useful review cases include insufficient stock, concurrent sales, date-range summaries, and a rejected write that must leave inventory unchanged. The existing API tests are a starting point; a production capacity claim would need a chosen database, transaction review, and measured workloads.

## 🚀 Features

- Product Management (`/products`)
- Inventory Tracking with Low Stock Alerts (`/inventory`)
- Inventory Logs (`/inventory/logs`)
- Sales Data Filtering & Creation (`/sales`)
- Revenue Summary by Interval (`/sales/summary`)
- Revenue by Category (`/sales/summary_by_category`)
- Current vs Previous Revenue Comparison (`/sales/compare`)
- Asynchronous MySQL Integration (via SQLAlchemy & aiomysql)
- Demo Data Seeder (`demo_data.py`)

---

## 🧱 Tech Stack

- **FastAPI** – High-performance API framework
- **SQLAlchemy (async)** – ORM
- **MySQL** – Relational database
- **Uvicorn** – ASGI server
- **Pydantic Settings** – Config management
- **Alembic** – (Optional) for migrations

---

## 🛠 Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/DevCipher-blip/ecommerce-admin-api.git
cd ecom-admin-api
```

### 2. Create Virtual Environment

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables

Create a `.env` file in the root directory:

```env
DATABASE_URL=mysql+aiomysql://root@localhost:3306/ecom_admin
```

### 5. Run Demo Seeder (for test data)

```bash
python -m demo_data
```

### 6. Start the Server

```bash
uvicorn app.main:app --reload
```

Visit: [http://localhost:8000/docs](http://localhost:8000/docs)

---

## 📘 API Reference

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/products` | GET | List all products |
| `/products` | POST | Create a product |
| `/inventory` | GET | List inventory (optionally low stock) |
| `/inventory` | POST | Add inventory entry |
| `/inventory/logs/{product_id}` | GET | View inventory change logs |
| `/sales` | GET | Filtered sales listing |
| `/sales` | POST | Create a sale |
| `/sales/summary` | GET | Revenue grouped by interval |
| `/sales/summary_by_category` | GET | Revenue by product category |
| `/sales/compare` | GET | Compare current vs previous revenue |
