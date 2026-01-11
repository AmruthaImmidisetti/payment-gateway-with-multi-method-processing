
# Payment Gateway with Multi-Method Processing and Hosted Checkout

This project implements a **mini payment gateway system** similar to Razorpay or Stripe.  
It supports **merchant onboarding, order creation, multi-method payments (UPI & Card), a hosted checkout page, and a merchant dashboard**, all running using **Docker Compose**.

This repository demonstrates real-world fintech concepts such as API authentication, payment validation, transaction lifecycle management, and frontend–backend integration.

---

## 🚀 Features

- Merchant authentication using **API Key & API Secret**
- Order creation and order status APIs
- Payment processing using:
  - **UPI** (with VPA validation)
  - **Card payments** (Luhn algorithm, card network detection, expiry validation)
- Hosted checkout page for customers
- Merchant dashboard with:
  - API credentials
  - Total transactions
  - Total amount
  - Success rate
  - Transaction history
- PostgreSQL database with proper schema and relationships
- Fully Dockerized setup
- Test mode for deterministic evaluation

---

## 🧱 Tech Stack

- **Backend**: Node.js / Java Spring Boot (REST API)
- **Frontend Dashboard**: React
- **Checkout Page**: React
- **Database**: PostgreSQL
- **Containerization**: Docker & Docker Compose

---

## 🗂️ Project Structure

```
payment-gateway-with-multi-method-processing/
├── backend/
├── frontend/
├── checkout-page/
├── Screenshots/
├── docker-compose.yml
├── .env.example
└── README.md
```

---

## ⚙️ How to Run This Project (Step-by-Step)

### 1️⃣ Prerequisites
Make sure you have the following installed:
- Docker
- Docker Compose
- Git

Verify installation:
```bash
docker --version
docker-compose --version
```

---

### 2️⃣ Clone the Repository
```bash
git clone https://github.com/AmruthaImmidisetti/payment-gateway-with-multi-method-processing.git
cd payment-gateway-with-multi-method-processing
```

---

### 3️⃣ Environment Configuration
Copy the example environment file:
```bash
cp .env.example .env
```

(Default values are sufficient for testing and evaluation.)

---

### 4️⃣ Start the Application
Run all services using a single command:
```bash
docker-compose up -d
```

Docker will start:
- PostgreSQL database
- Backend API service
- Merchant Dashboard
- Checkout Page

---

### 5️⃣ Access the Application

| Service | URL |
|------|------|
| API | http://localhost:8000 |
| Dashboard | http://localhost:3000 |
| Checkout Page | http://localhost:3001 |

---

## 🔑 Test Merchant Credentials (Auto-Seeded)

These credentials are automatically created when the application starts.

| Field | Value |
|------|------|
| Email | test@example.com |
| API Key | key_test_abc123 |
| API Secret | secret_test_xyz789 |

Use these credentials for dashboard login and API testing.

---

## 🔍 API Endpoints (Summary)

### Health Check
```
GET /health
```
Checks API and database connectivity.

### Create Order
```
POST /api/v1/orders
Headers:
X-Api-Key
X-Api-Secret
```

### Get Order
```
GET /api/v1/orders/{order_id}
```

### Create Payment
```
POST /api/v1/payments
```
Supports **upi** and **card** methods.

### Get Payment
```
GET /api/v1/payments/{payment_id}
```

---

## 💳 Payment Validation Logic

### UPI
- Validates VPA format (`username@bank`)
- Simulated success rate: **90%**

### Card
- Luhn algorithm validation
- Card network detection (Visa, Mastercard, Amex, RuPay)
- Expiry date validation
- Only last 4 digits stored (no CVV or full card numbers)
- Simulated success rate: **95%**

---

## 🖥️ Frontend Pages

### Merchant Dashboard (Port 3000)
- Login page
- Home dashboard with API credentials & statistics
- Transactions history page

### Checkout Page (Port 3001)
- Order summary
- Payment method selection
- UPI form
- Card form
- Processing state
- Success / Failure screens

---

## 🧪 Test Mode (For Evaluation)

Enable deterministic behavior using environment variables:
```
TEST_MODE=true
TEST_PAYMENT_SUCCESS=true
TEST_PROCESSING_DELAY=1000
```

This ensures predictable outcomes for automated evaluation.

---

## 📸 Screenshots

All required visual artifacts are available in the **Screenshots/** folder.

Included screenshots:
- API health check response
- Dashboard (before and after transactions)
- Transactions list (empty and populated)
- Checkout payment selection
- Card payment form
- Payment success screen

---

## 🎥 Video Demo

A complete end-to-end demo video is provided here:

🔗 **Video URL:**  
👉 https://drive.google.com/file/d/183JiEd1e83kk1QRmsA1ia_3-_sryrsso/view?usp=sharing

The video demonstrates:
1. Creating an order using the API
2. Opening the hosted checkout page
3. Completing payment (UPI/Card)
4. Viewing updated dashboard and transaction history

---

## 🧪 How to Test the Flow

1. Create an order using Postman or curl
2. Copy the returned `order_id`
3. Open:
```
http://localhost:3001/checkout?order_id=YOUR_ORDER_ID
```
4. Complete payment using:
   - UPI: `user@paytm`
   - Card: `4111 1111 1111 1111`, Expiry `12/26`, CVV `123`
5. Verify success in:
   - Checkout page
   - Dashboard
   - Transactions page

---

## 👤 Author

**Amrutha Immidisetti**  

---

⭐ This project was built to demonstrate **backend, frontend, and DevOps skills** through a real-world fintech payment gateway implementation.
