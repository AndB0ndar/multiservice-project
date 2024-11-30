### README.md

# Multi-Service Project: Product and Orders Services

This project is a microservices-based application consisting of two separate services:

1. **Product Service**: Manages goods and warehouses ([Repository](git@github.com:AndB0ndar/MSGoodsMIREA.git)).
2. **Orders Service**: Manages orders and tracks their statuses ([Repository](git@github.com:AndB0ndar/MSOrdersMIREA.git)).

Both services are implemented using **FastAPI** and **PostgreSQL** and are orchestrated using **Docker Compose**.

---

## Features

### Product Service
- Create, update, delete, and retrieve goods.
- Manage goods stored in warehouses.
- API Documentation: [http://localhost:8001/docs](http://localhost:8001/docs)

### Orders Service
- Create, update, delete, and retrieve orders.
- Track order statuses (e.g., pending, completed, canceled).
- API Documentation: [http://localhost:8002/docs](http://localhost:8002/docs)

---

## Prerequisites

Make sure you have the following installed on your machine:
- **Docker** (v20.10 or later)
- **Docker Compose** (v2.0 or later)
- Access to the repositories:
  - `git@github.com:AndB0ndar/MSGoodsMIREA.git`
  - `git@github.com:AndB0ndar/MSOrdersMIREA.git`

---

## Project Structure

```plaintext
project/
├── product_service/           # Cloned repository for product service
│   ├── app/                   # FastAPI application
│   ├── Dockerfile             # Dockerfile for product service
│   ├── requirements.txt       # Dependencies for product service
│   ├── .env                   # Environment variables for product service
├── orders_service/            # Cloned repository for orders service
│   ├── app/                   # FastAPI application
│   ├── Dockerfile             # Dockerfile for orders service
│   ├── requirements.txt       # Dependencies for orders service
│   ├── .env                   # Environment variables for orders service
├── docker-compose.yml         # Orchestration of services
└── README.md                  # Documentation
```

---

## Cloning the Repositories

1. Clone the **Product Service**:
   ```bash
   git clone git@github.com:AndB0ndar/MSGoodsMIREA.git product_service
   ```

2. Clone the **Orders Service**:
   ```bash
   git clone git@github.com:AndB0ndar/MSOrdersMIREA.git orders_service
   ```

---

## Environment Variables

Each service uses its own `.env` file for configuration. These files should be placed in the root of their respective service directories.

### Example `.env` for Product Service
```plaintext
DATABASE_URL=postgresql://user:password@goods_db:5432/goods_db
```

### Example `.env` for Orders Service
```plaintext
DATABASE_URL=postgresql://user:password@orders_db:5432/orders_db
```

---

## Getting Started

### Step 1: Build and Start Services
Use Docker Compose to build and start all services:
```bash
docker-compose up --build
```

### Step 2: Access the Services
- **Product Service**: [http://localhost:8001/docs](http://localhost:8001/docs)
- **Orders Service**: [http://localhost:8002/docs](http://localhost:8002/docs)

---

## API Endpoints

### README.md (Обновленная таблица эндпоинтов)

#### **Product Service Endpoints**

| Method | Endpoint                 | Description                             |
|--------|--------------------------|-----------------------------------------|
| GET    | `/products/`             | Retrieve a list of products. Supports pagination with `skip` and `limit`. |
| POST   | `/products/`             | Create a new product.                  |
| GET    | `/products/{product_id}` | Get details of a specific product by its ID. |
| DELETE | `/products/{product_id}` | Delete a product by its ID.            |

#### **Warehouse Endpoints**

| Method | Endpoint                     | Description                             |
|--------|------------------------------|-----------------------------------------|
| GET    | `/warehouses/`               | Retrieve a list of warehouses. Supports pagination with `skip` and `limit`. |
| POST   | `/warehouses/`               | Create a new warehouse.                |
| GET    | `/warehouses/{warehouse_id}` | Get details of a specific warehouse by its ID. |
| DELETE | `/warehouses/{warehouse_id}` | Delete a warehouse by its ID.          |

---

#### **Orders Service Endpoints**

| Method | Endpoint                 | Description                             |
|--------|--------------------------|-----------------------------------------|
| POST   | `/orders/`               | Create a new order.                     |
| GET    | `/orders/`               | Retrieve a list of orders. Supports pagination with `skip` and `limit`. |
| GET    | `/orders/{order_id}`     | Get details of a specific order by its ID. |
| PATCH  | `/orders/{order_id}`     | Update the status of an order (e.g., "completed", "canceled"). | 

--- 

#### Notes

1. **Pagination**: For all endpoints with pagination support, parameters are used:
   - `skip` (int): How many records to skip (default is `0`).
   - `limit` (int): Maximum number of records in the response (default is `10`).

2. **Response codes**:
   - **200**: Successful operation.
   - **201**: Resource successfully created (e.g. for POST).
   - **404**: Resource not found (e.g., for an invalid `ID`).
   - **400**: Incorrect data or request parameters.

---

## Development

### Running Locally
To run the services locally (outside Docker):
1. Clone the repositories as described above.
2. Set up PostgreSQL databases and update the `.env` files accordingly.
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Start the FastAPI server:
   ```bash
   uvicorn app.main:app --reload
   ```

