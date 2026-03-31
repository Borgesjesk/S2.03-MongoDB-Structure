# Nivel 1 - Optic Store

MongoDB schema design for an optic store, explored from two different modeling perspectives.

## Exercise 1 — Client Perspective (`ex1/src/`)

The **customer** is the central document. All collections are normalized and linked via references (`objectId`).

| File | Collection | Description |
|------|-----------|-------------|
| `customers.json` | `customers` | Client profile with address and optional referral |
| `employee.json` | `employees` | Staff member with store assignment and role |
| `glasses.json` | `glasses` | Product with prescription data and provider reference |
| `provider.json` | `providers` | Glasses supplier with address and tax info |
| `sales.json` | `sales` | Transaction linking customer, glasses and employee |

### Relationships (ex1)
```
customers ──referredBy──> customers
sales ──customerId──> customers
sales ──glassesId──> glasses
sales ──employeeId──> employees
glasses ──providerId──> providers
employees ──storeId──> (store collection)
```

## Exercise 2 — Glasses Perspective (`ex2/src/`)

The **glasses** document is the root entity. Provider data is embedded directly in the glasses document and a sales history array is maintained inline. Sales documents also embed a customer snapshot.

| File | Collection | Description |
|------|-----------|-------------|
| `glasses.json` | `glasses` | Root entity with embedded provider snapshot and sales history |
| `provider.json` | `providers` | Full provider record (source of truth for embedded data) |
| `sales.json` | `sales` | Sale with embedded customer snapshot for historical accuracy |
| `customers.json` | `customers` | Customer master record |
| `employee.json` | `employees` | Staff member record |

### Modeling trade-offs (ex2 vs ex1)
- **Reads are faster**: no joins needed to get glasses + provider info
- **Writes are more complex**: updating a provider requires updating all embedded copies
- **Sales history** on the glasses document enables timeline queries without aggregation

## Running

```bash
docker-compose up -d
```

MongoDB will be available at `mongodb://admin:admin123@localhost:27017`
Mongo Express UI at `http://localhost:8081`

## Apply a schema validator

```javascript
db.createCollection("glasses", {
  validator: { /* paste contents of glasses.json here */ }
})
```

## 🚀 Installation and Execution
```bash
git clone https://github.com/Borgesjesk/S2.03-MongoDB-Structure.git
```
