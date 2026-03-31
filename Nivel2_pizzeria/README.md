# Nivel 2 - Pizzeria Delivery

MongoDB schema design for a multi-store pizzeria delivery management system.

## Collections (`src/`)

| File | Collection | Description |
|------|-----------|-------------|
| `customers.json` | `customers` | Registered customers with default delivery address |
| `employees.json` | `employees` | Staff with role (cook / delivery / manager) and vehicle info |
| `products.json` | `products` | Menu items: pizzas, drinks, desserts, sides |
| `stores.json` | `stores` | Physical pizzeria branches with opening hours |
| `orderDetails.json` | `orderDetails` | Full order transaction with items, delivery info and status |

## Relationships

```
orderDetails ──customerId──> customers
orderDetails ──storeId──> stores
orderDetails ──items[].productId──> products
orderDetails ──deliveryEmployeeId──> employees
employees ──storeId──> stores
```

## Key design decisions

- **Items are embedded** in `orderDetails` with a price snapshot — this preserves the price at the time of purchase even if the product price changes later.
- **Delivery address** is copied to the order so historical orders show where they were delivered, not the customer's current address.
- **Order status** follows the lifecycle: `pending → preparing → out_for_delivery → delivered` (or `cancelled`).

## Running

```bash
docker-compose up -d
```

MongoDB at `mongodb://admin:admin123@localhost:27018`
Mongo Express UI at `http://localhost:8082`

> Port 27018 / 8082 are used to avoid conflicts if Nivel1 is also running.

## Apply a schema validator example

```javascript
db.createCollection("orderDetails", {
  validator: { /* paste contents of orderDetails.json here */ },
  validationLevel: "strict",
  validationAction: "error"
})
```
