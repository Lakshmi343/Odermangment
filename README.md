# Odermangment
# Order Management System API Documentation

This API provides role-based authentication and product management for the Order Management System. Users can register, log in, and manage products based on their roles (Manufacturer, Seller, Customer).

## Authentication API

### Register a User (Seller or Manufacturer)
**Endpoint:** `POST /api/auth/register`

**Request Body:**
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123",
  "role": "manufacturer"
}
```

**Response:**
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjY3Yzk3YmM0Y2FiNDExMjhmOGEyNGIzNyIsImlhdCI6MTc0MTI3OTg2NiwiZXhwIjoxNzQxMjgzNDY2fQ._towbVaFfhaTOiP_GJKXSjm5fYesv8V4BeLc6HsYWiQ"
}
```

---

## Product Management

###A Add Product
**Endpoint:** `POST /api/products/add`

**Request Body:**
```json
{
  "name": "iPhone 13 Pro",
  "description": "Apple iPhone 13 Pro with A15 Bionic chip, 6.1-inch Super Retina XDR display, ProMotion, and triple-camera system.",
  "quantity": 50,
  "price": 999
}
```

**Headers:**
```
Authorization: Bearer <token>
```

**Response:**
```json
{
  "name": "iPhone 13 Pro",
  "description": "Apple iPhone 13 Pro with A15 Bionic chip, 6.1-inch Super Retina XDR display, ProMotion, and triple-camera system.",
  "status": "available",
  "quantity": 50,
  "price": 999,
  "createdBy": "67c97bc4cab41128f8a24b37",
  "_id": "67c9d74a15b161f446778a74",
  "__v": 0
}
```

###B Change Product Status
**Endpoint:** `PUT /api/products/67c9d74a15b161f446778a74/status`

**Request Body:**
```json
{
  "status": "faulty"
}
```

**Response:**
```json
{
  "_id": "67c9d74a15b161f446778a74",
  "name": "iPhone 13 Pro",
  "description": "Apple iPhone 13 Pro with A15 Bionic chip, 6.1-inch Super Retina XDR display, ProMotion, and triple-camera system.",
  "status": "faulty",
  "quantity": 50,
  "price": 999,
  "createdBy": "67c97bc4cab41128f8a24b37",
  "__v": 0,
  "lastUpdatedBy": "67c97bc4cab41128f8a24b37"
}
```

###C Get Faulty Products with Last Updated Details
**Endpoint:** `GET /api/products/faulty`

**Response:**
```json
[
  {
    "_id": "67c9d74a15b161f446778a74",
    "name": "iPhone 13 Pro",
    "description": "Apple iPhone 13 Pro with A15 Bionic chip, 6.1-inch Super Retina XDR display, ProMotion, and triple-camera system.",
    "status": "faulty",
    "quantity": 50,
    "price": 999,
    "createdBy": "67c97bc4cab41128f8a24b37",
    "__v": 0,
    "lastUpdatedBy": {
      "_id": "67c97bc4cab41128f8a24b37",
      "name": "John Doe",
      "email": "john@example.com",
      "role": "manufacturer"
    }
  }
]
```

---

## Order Management

### Create Order
**Endpoint:** `POST /api/orders`

**Request Body:**
```json
{
  "product": "64f1b2c8e4b0f5a3d4e5f6a7",
  "seller": "67c98bc0d59425364edc6d4a",
  "manufacturer": "67c97bc4cab41128f8a24b37",
  "customer": "67c98c0ad59425364edc6d4d",
  "quantity": 5,
  "totalPrice": 500
}
```

**Response:**
```json
{
  "product": "64f1b2c8e4b0f5a3d4e5f6a7",
  "seller": "67c98bc0d59425364edc6d4a",
  "manufacturer": "67c97bc4cab41128f8a24b37",
  "customer": "67c98c0ad59425364edc6d4d",
  "quantity": 5,
  "totalPrice": 500,
  "_id": "67c9e015abf1ed319f34e4b3",
  "orderDate": "2025-03-06T17:49:09.380Z",
  "__v": 0
}
```

###D Get All Orders with Details
**Endpoint:** `GET /api/orders`

**Response:**
```json
{
  "orders": [
    {
      "_id": "67c9e015abf1ed319f34e4b3",
      "product": null,
      "seller": {
        "_id": "67c98bc0d59425364edc6d4a",
        "name": "Lakshmi",
        "email": "lakshminairkalleri@gamil.com"
      },
      "manufacturer": {
        "_id": "67c97bc4cab41128f8a24b37",
        "name": "John Doe",
        "email": "john@example.com"
      },
      "customer": {
        "_id": "67c98c0ad59425364edc6d4d",
        "name": "customer",
        "email": "customer@gamil.com"
      },
      "quantity": 5,
      "totalPrice": 500,
      "orderDate": "2025-03-06T17:49:09.380Z",
      "__v": 0
    }
  ],
  "totalOrders": 1,
  "page": 1,
  "limit": 10
}
```

###E Get Most Ordered Products (Descending Order)
**Endpoint:** `GET /api/orders/most-ordered`

**Response:**
```json
[
  {
    "product": "Product 1",
    "totalOrders": 10
  }
]
```

###F Get Total Orders & Revenue by Month
**Endpoint:** `GET /api/orders/revenue-by-month`

**Response:**
```json
[
  {
    "_id": 3,
    "totalOrders": 1,
    "totalRevenue": 500
  }
]
```

