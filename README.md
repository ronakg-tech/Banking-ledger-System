# 🏦 Banking Ledger System

A **high-performance, secure, and scalable banking backend** built using **Node.js, Express, and MongoDB**.

This system implements a **Double-Entry Ledger Architecture** to ensure **financial accuracy, consistency, and reliability**.

---

## 🌟 Core Features

### 🔹 Immutable Ledger System
- No static balance stored
- Real-time balance calculated using MongoDB Aggregation Pipelines  
- **Formula:** `Total Credits - Total Debits`
- Ledger entries are immutable (`immutable: true`) to prevent tampering

---

### 🔹 Atomic Transactions (ACID)
- Uses MongoDB Sessions & Transactions
- Ensures:
  - Debit Sender  
  - Credit Receiver  
  - Update Status  
- ✅ Either all succeed **OR** all fail (no partial updates)

---

### 🔹 Idempotency Protection
- Prevents duplicate payments
- Uses **Idempotency Keys (UUID)**
- Handles:
  - Network retries  
  - Double-click issues  

---

### 🔹 Security Implementation
- JWT Authentication + HTTP-Only Cookies  
- Token Blacklisting (Logout invalidates tokens)  
- TTL Index (auto delete in 3 days)  

#### 🔐 Password Security
- Uses `bcryptjs`
- Salt rounds for strong hashing

---

### 🔹 Email Integration
- Integrated **Nodemailer with Google OAuth2**
- Sends:
  - Welcome emails  
  - Transaction success notifications  

---

### 🔹 Database Optimization
- Efficient Indexing & Compound Indexes  
- Optimized queries on:
  - `userId`
  - `status`

---

### 📂 Project Structure

src/
├── config/ # DB & environment setup
├── controllers/ # Request handling logic
├── middlewares/ # Auth, validation, idempotency
├── models/ # Mongoose schemas
├── routes/ # API routes
├── services/ # Email & external integrations


---

## 🚀 Setup & Installation

### 1️⃣ Environment Variables (`.env`)


MONGO_URI=
JWT_SECRET=
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
GOOGLE_REFRESH_TOKEN=
EMAIL_USER=


---

### 2️⃣ Run Commands

#### Install dependencies
```bash
npm install
Development
npm run dev
Production
npm start
```

###🛣️ API Endpoints
## 🔐 Authentication
POST   /api/auth/register   → Register user + send email  
POST   /api/auth/login      → Login & get JWT  
POST   /api/auth/logout     → Logout & blacklist token  
## 💳 Accounts
POST   /api/accounts/                      → Create account  
GET    /api/accounts/                      → Get user accounts  
GET    /api/accounts/balance/:accountId    → Get dynamic balance  
## 💸 Transactions
POST   /api/transactions/                      → P2P transfer (atomic + idempotent)  
POST   /api/transactions/system/initial-funds  → Admin funding  
### 🛡️ Transaction Flow
 1️⃣ Validate
Input validation
Authentication
Idempotency check
 2️⃣ Initialize
Create pending transaction
 3️⃣ Process
Start MongoDB session
Debit + Credit ledger entries
 4️⃣ Finalize
Commit transaction
Mark as completed
###⚠️ Important Notes
-Add .env and node_modules to .gitignore
-Deployment (e.g., Render)
-node server.js
### 🎯 Key Highlights
-✅ Real-world banking-grade architecture
-🔐 Strong focus on data integrity & security
-⚡ Scalable and production-ready backend design
-🤝 Contributing

## Contributions are welcome!
Feel free to fork the repo and submit a pull request.

