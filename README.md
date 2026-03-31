# S2.03 - MongoDB Structure

This project explores MongoDB document modeling and schema design across two exercises.

## Structure

```
S2.03-MongoDB-Structure/
├── Nivel1_opticStore/      # Optic store schema design
│   ├── ex1/src/            # Client-perspective schema
│   ├── ex2/src/            # Glasses-perspective schema
│   ├── docker-compose.yml
│   └── README.md
├── Nivel2_pizzeria/        # Pizzeria delivery schema design
│   ├── src/
│   ├── docker-compose.yml
│   └── README.md
└── README.md
```

## Levels

### Nivel 1 - Optic Store
Two approaches to modeling the same domain:
- **ex1**: Data modeled from the **client** point of view (normalized, client is the root document)
- **ex2**: Data modeled from the **glasses** point of view (glasses is the root document, with embedded data)

### Nivel 2 - Pizzeria
Delivery management system for a pizzeria chain with stores, employees, products, customers and orders.

## Running

Each level has its own `docker-compose.yml`. Start MongoDB with:

```bash
cd Nivel1_opticStore
docker-compose up -d

# or

cd Nivel2_pizzeria
docker-compose up -d
```
