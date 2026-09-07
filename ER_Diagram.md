Business Structure
|     |     | BUSINESS |     | STORE |     |     |     | USER |     |     |     |
| --- | --- | -------- | --- | ----- | --- | --- | --- | ---- | --- | --- | --- |
Leyenda
|     |            | business_id | PK        | store_id    | PK        | USER_STORE |     | user_id       | PK        |     |     |
| --- | ---------- | ----------- | --------- | ----------- | --------- | ---------- | --- | ------------- | --------- | --- | --- |
|     | Primaria   | name        | TEXT      | business_id | FK        | user_id    | FK  | business_id   | FK        |     |     |
|     | Secundaria | address     | TEXT      | name        | TEXT      | store_id   | FK  | name          | TEXT      |     |     |
|     | Intermedia | created_at  | TIMESTAMP | adress      | TEXT      |            |     | email         | TEXT      |     |     |
|     |            | tax_id      | INT       | phone       | TEXT      |            |     | password_hash | TEXT      |     |     |
|     |            |             |           | created_at  | TIMESTAMP |            |     | role          | TEXT      |     |     |
|     |            |             |           | active      | BOOLEAN   |            |     | active        | BOOLEAN   |     |     |
|     |            |             |           |             |           |            |     | created_at    | TIMESTAMP |     |     |
Purchases
| CATEGORY    |     | PRODUCT    |     |     |     |     |     |          |     |         |     |
| ----------- | --- | ---------- | --- | --- | --- | --- | --- | -------- | --- | ------- | --- |
|             |     |            |     |     |     |     |     | PURCHASE |     | SUPLIER |     |
| category_id | PK  | product_id | PK  |     |     |     |     |          |     |         |     |
STORE_PRODUCT
| business_id | FK   | business_id | FK   |            |     |     |     | purchase_id | PK  | suplier_id  | PK   |
| ----------- | ---- | ----------- | ---- | ---------- | --- | --- | --- | ----------- | --- | ----------- | ---- |
| name        | TEXT | sku         | TEXT | store_id   | FK  |     |     | business_id | FK  | business_id | FK   |
|             |      | name        | TEXT | product_id | FK  |     |     | store_id    | FK  | name        | TEXT |
MANUFACTURER
|     |     | description | TEXT | quantity | INT |     |     | user_id | FK  | tax_id | INT |
| --- | --- | ----------- | ---- | -------- | --- | --- | --- | ------- | --- | ------ | --- |
manufacturer_id PK category_id FK minimum_quantity INT Every inventory movement suplier_id FK phone TEXT
updates the store product
business_id FK manufacturer_id FK maximun_quantity INT purchase_date TIMESTAMP email TEXT
| name  | TEXT | unit_price | NUM       |     |     |     |     | subtotal | NUM  | adress | TEXT    |
| ----- | ---- | ---------- | --------- | --- | --- | --- | --- | -------- | ---- | ------ | ------- |
|       |      | unit       | TEXT      |     |     |     |     |          |      |        |         |
| phone | TEXT |            |           |     |     |     |     | tax      | NUM  | active | BOOLEAN |
|       |      | active     | BOOLEAN   |     |     |     |     | status   | TEXT |        |         |
|       |      | created_at | TIMESTAMP |     |     |     |     |          |      |        |         |
Sales
Every time a price changes,
|     |     |     |     |     |     | INVENTORY_MOVEMENT |     | PURCHASE_ITEM |     |     |     |
| --- | --- | --- | --- | --- | --- | ------------------ | --- | ------------- | --- | --- | --- |
it creates a new entry
|     |     |     |     |     |     | movement_id | PK  | purchase_item_id | PK  |     |     |
| --- | --- | --- | --- | --- | --- | ----------- | --- | ---------------- | --- | --- | --- |
in price_history
|     |     | CUSTOMER    |     | SALE        |     | store_id   | FK  | purchase_id | FK  |     |     |
| --- | --- | ----------- | --- | ----------- | --- | ---------- | --- | ----------- | --- | --- | --- |
|     |     |             |     |             |     | product_id | FK  | product_id  | FK  |     |     |
|     |     | customer_id | PK  | sale_id     | PK  |            |     |             |     |     |     |
|     |     |             |     |             |     | user_id    | FK  | quantity    | INT |     |     |
|     |     | business_id | FK  | business_id | FK  |            |     |             |     |     |     |
PRICE_HISTORY
|                  |     |                |      |             |           | movement_type | TEXT      | unit_cost                 | NUM |     |     |
| ---------------- | --- | -------------- | ---- | ----------- | --------- | ------------- | --------- | ------------------------- | --- | --- | --- |
|                  |     | name           | TEXT | store_id    | FK        |               |           |                           |     |     |     |
| price_history_id | PK  |                |      |             |           | quantity      | INT       | subtotal                  | NUM |     |     |
|                  |     | identification | INT  | user_id     | FK        |               |           |                           |     |     |     |
| product_id       | FK  |                |      |             |           | created_at    | TIMESTAMP |                           |     |     |     |
|                  |     | phone          | TEXT | customer_id | FK        |               |           |                           |     |     |     |
| price            | NUM |                |      |             |           |               |           | Every purchase creates an |     |     |     |
|                  |     | email          | TEXT | sale_date   | TIMESTAMP |               |           |                           |     |     |     |
valid_from DATE created_at TIMESTAMP subtotal NUM inventory movement
| valid_to | DATE |     |     |                |      |     |     |     |     |     |     |
| -------- | ---- | --- | --- | -------------- | ---- | --- | --- | --- | --- | --- | --- |
|          |      |     |     | discount       | NUM  |     |     |     |     |     |     |
|          |      |     |     | tax            | NUM  |     |     |     |     |     |     |
|          |      |     |     | payment_method | TEXT |     |     |     |     |     |     |
|          |      |     |     | status         | TEXT |     |     |     |     |     |     |
OTHER_MOVEMENTS
Every sale creates an
|     |     |     |     |     |     | inventory movement |     | movement_id | PK  |     |     |
| --- | --- | --- | --- | --- | --- | ------------------ | --- | ----------- | --- | --- | --- |
|     |     |     |     |     |     |                    |     | store_id    | FK  |     |     |
|     |     |     |     |     |     |                    |     | product_id  | FK  |     |     |
SALE_ITEM
|     |     |     |     |              |     |     |     | quantity                            | INT  |     |     |
| --- | --- | --- | --- | ------------ | --- | --- | --- | ----------------------------------- | ---- | --- | --- |
|     |     |     |     | sale_item_id | PK  |     |     |                                     |      |     |     |
|     |     |     |     |              |     |     |     | movement_type                       | TEXT |     |     |
|     |     |     |     | sale_id      | FK  |     |     |                                     |      |     |     |
|     |     |     |     | product_id   | FK  |     |     | There can be other types of product |      |     |     |
movement such as transfers between
|     |     |     |     | quantity   | INT |     |     |                            |     |     |     |
| --- | --- | --- | --- | ---------- | --- | --- | --- | -------------------------- | --- | --- | --- |
|     |     |     |     | unit_price | NUM |     |     | stores or expired products |     |     |     |
|     |     |     |     | discount   | NUM |     |     |                            |     |     |     |
|     |     |     |     | subtotal   | NUM |     |     |                            |     |     |     |