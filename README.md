# Pharmacy Inventory & Sales Management System

**Course:** C11665 - DPR400210: Database Programming
**Instructor:** Eric Maniraguha
**Assignment:** Group Assignment III — Design and Implementation of a Simple Database Application Using PL/SQL

**Group Members:**
| # | Student ID |
|---|------|-----------|
| 1 | 29761/2025
| 2 | 31527/2025
| 3 | 32239/2025
| 4 | 32135/2025
| 5 | 31383/2025

---

## 1. Problem Definition

Small pharmacies often manage stock and sales manually, which leads to:
- Running out of critical medicines without warning (stockouts)
- No easy way to see which medicines generate the most revenue
- No automated, consistent way to record a sale and update stock at the same time

This project models a **Pharmacy Inventory & Sales Management System** that tracks suppliers, medicines, stock levels, and sales, then uses PL/SQL to automate sales processing, stock control, and reporting — so pharmacy staff can make faster, data-driven decisions.

## 2. Database Design

### Entity Relationship Overview
```
SUPPLIERS (1) ----< (M) MEDICINES (1) ---- (1) STOCK
                          |
                          | (1)
                          |
                        (M) SALES
```

### Tables
| Table | Description |
|---|---|
| `suppliers` | Companies that supply medicines to the pharmacy |
| `medicines` | Catalog of medicines, price, category, and expiry date |
| `stock` | Current quantity available per medicine and its reorder threshold |
| `sales` | Transaction log of every medicine sold |

See [`01_schema_and_data.sql`](01_schema_and_data.sql) for full DDL and sample data.

## 3. PL/SQL Components

| Concept | Object | File | What it does |
|---|---|---|---|
| **Function** | `fn_get_unit_price` | `02_functions.sql` | Returns unit price of a medicine |
| **Function** | `fn_total_revenue` | `02_functions.sql` | Returns total revenue earned by a medicine |
| **Function** | `fn_stock_status` | `02_functions.sql` | Returns `LOW STOCK` or `SUFFICIENT` |
| **Stored Procedure** | `sp_add_sale` | `03_procedures.sql` | Records a sale, computes total, decreases stock, handles insufficient-stock errors |
| **Stored Procedure** | `sp_restock_medicine` | `03_procedures.sql` | Increases stock quantity and updates restock date |
| **Window Functions** | 5 queries | `04_window_functions.sql` | `RANK`, `DENSE_RANK`, running totals (`SUM() OVER`), `LAG`/`LEAD`, `PARTITION BY` for per-category ranking, percentage-of-total |
| **Anonymous Blocks** | 3 blocks | `05_anonymous_blocks.sql` | Cursor-driven stock alert report, exception-handling demo, revenue summary report |

## 4. How to Run

1. Connect to an Oracle database (e.g. via SQL*Plus, SQL Developer, or Oracle Live SQL).
2. Run the scripts **in this exact order**:
   ```
   01_schema_and_data.sql
   02_functions.sql
   03_procedures.sql
   04_window_functions.sql
   05_anonymous_blocks.sql
   ```
3. Make sure `SET SERVEROUTPUT ON;` is enabled to see `DBMS_OUTPUT` messages from the procedures and anonymous blocks.

## 5. Repository Setup Checklist (for submission)

- [ ] Create **one** GitHub repository for the group
- [ ] Add all 5 group members as collaborators (Settings → Collaborators)
- [ ] Push all `.sql` files and this `README.md`
- [ ] Confirm every member understands **every part** of the code — grading is individual during the Tuesday presentation
- [ ] Submit the repository link via the Google Form before **14:00 today**

## 6. Presentation Notes

Each member should be ready to explain, in their own words:
- Why this problem matters and how the schema models it
- What each function/procedure does and why exceptions are handled the way they are
- What each window function query reveals that a normal `GROUP BY` query cannot

