

## **🛒 Microservices & Their APIs**  

### **1️⃣ User Service (Authentication & User Management)**
Handles user authentication, registration, and profile management.

#### **APIs:**  
🔹 **User Registration**  
```http
POST /api/users/register
```
📌 **Request Body:**  
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "securepassword"
}
```
📌 **Response:**  
```json
{
  "userId": "12345",
  "message": "User registered successfully"
}
```

🔹 **User Login**  
```http
POST /api/users/login
```
📌 **Request Body:**  
```json
{
  "email": "john@example.com",
  "password": "securepassword"
}
```
📌 **Response:**  
```json
{
  "token": "jwt_token_here",
  "expiresIn": 3600
}
```

🔹 **Get User Profile** (Protected API)  
```http
GET /api/users/profile
```
📌 **Headers:** `Authorization: Bearer jwt_token_here`  
📌 **Response:**  
```json
{
  "userId": "12345",
  "name": "John Doe",
  "email": "john@example.com"
}
```

---

### **2️⃣ Product Service**
Manages product catalog, details, and inventory.

#### **APIs:**  
🔹 **Get All Products**  
```http
GET /api/products
```
📌 **Response:**  
```json
[
  {
    "productId": "p1",
    "name": "Laptop",
    "price": 1000,
    "stock": 20
  },
  {
    "productId": "p2",
    "name": "Smartphone",
    "price": 500,
    "stock": 15
  }
]
```

🔹 **Get Product by ID**  
```http
GET /api/products/{productId}
```
📌 **Response:**  
```json
{
  "productId": "p1",
  "name": "Laptop",
  "description": "High-end gaming laptop",
  "price": 1000,
  "stock": 20
}
```

🔹 **Add a New Product (Admin Only)**  
```http
POST /api/products
```
📌 **Request Body:**  
```json
{
  "name": "Headphones",
  "description": "Wireless noise-canceling headphones",
  "price": 150,
  "stock": 50
}
```
📌 **Response:**  
```json
{
  "productId": "p3",
  "message": "Product added successfully"
}
```

---

### **3️⃣ Order Service**
Handles order placement, order tracking, and history.

#### **APIs:**  
🔹 **Place an Order**  
```http
POST /api/orders
```
📌 **Request Body:**  
```json
{
  "userId": "12345",
  "products": [
    { "productId": "p1", "quantity": 1 },
    { "productId": "p2", "quantity": 2 }
  ],
  "totalAmount": 2000
}
```
📌 **Response:**  
```json
{
  "orderId": "o98765",
  "message": "Order placed successfully"
}
```

🔹 **Get Order by ID**  
```http
GET /api/orders/{orderId}
```
📌 **Response:**  
```json
{
  "orderId": "o98765",
  "userId": "12345",
  "products": [
    { "productId": "p1", "name": "Laptop", "quantity": 1, "price": 1000 },
    { "productId": "p2", "name": "Smartphone", "quantity": 2, "price": 500 }
  ],
  "totalAmount": 2000,
  "status": "Processing"
}
```

🔹 **Get Order History (User Specific)**  
```http
GET /api/orders/user/{userId}
```
📌 **Response:**  
```json
[
  {
    "orderId": "o98765",
    "totalAmount": 2000,
    "status": "Processing"
  },
  {
    "orderId": "o12345",
    "totalAmount": 500,
    "status": "Delivered"
  }
]
```

---

### **4️⃣ Payment Service**
Handles payments and transactions.

#### **APIs:**  
🔹 **Initiate Payment**  
```http
POST /api/payments
```
📌 **Request Body:**  
```json
{
  "orderId": "o98765",
  "userId": "12345",
  "paymentMethod": "credit_card"
}
```
📌 **Response:**  
```json
{
  "paymentId": "pay001",
  "status": "Success"
}
```

🔹 **Get Payment Status**  
```http
GET /api/payments/{paymentId}
```
📌 **Response:**  
```json
{
  "paymentId": "pay001",
  "status": "Success",
  "amount": 2000
}
```

---

### **5️⃣ Notification Service**
Sends order status updates to users.

#### **APIs:**  
🔹 **Send Notification**  
```http
POST /api/notifications
```
📌 **Request Body:**  
```json
{
  "userId": "12345",
  "message": "Your order has been shipped!"
}
```
📌 **Response:**  
```json
{
  "notificationId": "n001",
  "status": "Sent"
}
```
