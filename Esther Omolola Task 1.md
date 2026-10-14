# E-commerce Orders Dataset (Cleaned)

A cleaned dataset of 1,200 e-commerce orders placed between **1 January 2023 and 30 June 2025**. It was prepared for a data analytics project and is ready for exploration, SQL practice, and visualisation.

**File:** `Dataset_for_Data_Analytics_-_cleaned.csv`

## Dataset at a glance

| | |
|---|---|
| Rows | 1,200 orders (one row per order) |
| Columns | 17 |
| Period covered | 2023-01-01 to 2025-06-30 |
| Products | 7 (Chair, Desk, Laptop, Monitor, Phone, Printer, Tablet) |
| Missing values | Only `CouponCode` (309 blanks, meaning no coupon was used) |
| Duplicate order IDs | None |

## Data dictionary

| Column | Type | Description |
|---|---|---|
| `OrderID` | text | Unique order identifier (e.g. `ORD200000`) |
| `Date` | date | Order date, in `M/D/YYYY` format |
| `Year` | integer | Year of the order (2023, 2024, 2025) |
| `Quarter` | text | Calendar quarter of the order (`Q1` to `Q4`) |
| `CustomerID` | text | Customer identifier (e.g. `C72649`) |
| `Product` | text | Product ordered |
| `Quantity` | integer | Units ordered (1 to 5) |
| `UnitPrice` | decimal | Price per unit (11.39 to 699.93) |
| `ShippingAddress` | text | Shipping street address |
| `PaymentMethod` | text | `Cash`, `Credit Card`, `Debit Card`, `Gift Card`, `Online` |
| `OrderStatus` | text | `Delivered`, `Shipped`, `Pending`, `Cancelled`, `Returned` |
| `TrackingNumber` | text | Unique shipment tracking number (e.g. `TRK37947903`) |
| `ItemsInCart` | integer | Number of items in the cart at checkout (1 to 10) |
| `CouponCode` | text | `SAVE10`, `FREESHIP`, `WINTER15`, or blank if none |
| `ReferralSource` | text | `Email`, `Facebook`, `Google`, `Instagram`, `Referral` |
| `TotalPrice` | decimal | `Quantity` x `UnitPrice` |
| `TotalRevenue` | decimal | Derived column used as a sanity check against `TotalPrice` (see notes below) |

## Data cleaning (Power Query)

The raw data was cleaned in Excel Power Query:

1. **Removed duplicate rows.**
2. **Converted the `Date` column** from text to a proper date type.
3. **Created `Year` and `Quarter`** from `Date` to make it easier to analyse trends over time.
4. **Created `TotalRevenue`** as a sanity check against `TotalPrice`. The two columns match in every row, which confirms the totals are consistent.

## Things to know before analysing

- `TotalPrice` always equals `Quantity` x `UnitPrice`.
- `TotalRevenue` is a validation column and is identical to `TotalPrice`, so use one or the other, not both. Cancelled and returned orders still carry a value, so filter on `OrderStatus` if you want revenue from completed orders only.
- `Year` and `Quarter` are consistent with `Date` in every row.
- `CouponCode` blanks are genuine "no coupon" values, not data errors.
- 11 customer IDs appear more than once, so a customer can have multiple orders.

## Example questions to explore

- What is the total revenue by year, quarter, and product?
- Which referral sources and coupon codes bring in the most orders?
- What share of orders are cancelled or returned, and does it vary by product or payment method?
- What are the mean and median order values, and which orders are outliers?

## Tools used

- Excel and Power Query for data cleaning
- PostgreSQL (Supabase) for SQL analysis

## Author

Your name: [@highflyer001](https://github.com/highflyer001)
