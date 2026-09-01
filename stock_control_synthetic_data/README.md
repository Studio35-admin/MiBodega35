# Synthetic Stock Control System Dataset

Generated to match the uploaded ER diagram. 1 business, 4 stores, 18 months
of data (2024-06-01 to 2025-11-30).

## Files
| File | Rows | Notes |
|---|---|---|
| business.csv | 1 | |
| store.csv | 4 | flagship, mall, suburban, small kiosk |
| category.csv | 6 | |
| manufacturer.csv | 8 | |
| product.csv | 60 | 10 per category |
| user.csv | 12 | employees |
| user_store.csv | 14 | assignments |
| customer.csv | 300 | ~12% missing phone/email |
| suplier.csv | 10 | (spelling matches schema) |
| price_history.csv | 64 | includes mid-period increases |
| sale.csv | 32,462 | |
| sale_item.csv | 96,956 | |
| purchase.csv | 144 | biweekly per store |
| purchase_item.csv | 2,058 | |
| inventory_movement.csv | 99,014 | sale + purchase movements |
| other_movements.csv | 150 | transfers, expired, damaged |
| store_product.csv | 240 | current stock, derived from movements |

## Embedded patterns (your "answer key" — don't peek until after your first analysis pass)

1. **Holiday seasonality**: all categories get a demand bump in Nov (+30%) and Dec (+60%).
2. **Home Appliances decline**: category_id=3 demand linearly decays to ~50% of its
   starting level by the end of the 18 months (aging product line).
3. **Suburban Branch stockout**: store_id=3, Feb 10-28 2025 — demand drops to 15%,
   then partially recovers (60%) through mid-March before returning to normal.
4. **Beverages discount campaign**: category_id=1, Jul-Aug 2025 — 20% line-item
   discount, demand multiplier x1.8 (volume up, margin down).
5. **Price increase response**: products [22, 38, 23, 26] get a price increase on
   2025-03-01. Demand drops sharply for 30 days after (x0.6), then partially
   recovers (x0.85) for the following 90 days.

## Deliberate messiness
- ~12% of customers have missing phone and/or email.
- ~4% of sale timestamps are stored as `DD/MM/YYYY HH:MM` instead of
  `YYYY-MM-DD HH:MM:SS` — a real-world inconsistent-format problem.
- ~2% of sales have a near-duplicate sale (same store/customer/items, a few
  minutes apart) — simulates double-submitted transactions.
- `store_product.quantity` is derived from starting stock + purchases - sales
  + other movements, so if your own reconciliation math doesn't match exactly,
  check your join logic before assuming the data's wrong.

## Schema quirks kept as-is (matching your ER diagram)
- `suplier`, `adress`, `maximun_quantity` are spelled as in the original diagram.
- `sale.discount` and `sale_item.discount` both exist — campaign discounts were
  applied at the line-item level (sale_item.discount), sale.discount is 0
  throughout this dataset (a case for you to decide how to interpret if it
  comes up).
