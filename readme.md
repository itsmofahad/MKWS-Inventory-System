
---

# 🗃 MKWS Inventory System


# 🗃 .....................

Inventory Management System for **Muslim Khatri Medical & Diagnostic Center**
Built with **React + Redux Toolkit (frontend)** and **Node.js + Express + MongoDB (backend)**.

---




```markdown
## 📦 Install & Setup MongoDB

This project requires **MongoDB** (tested with version 4.2+) installed on your system.

### 1. Install MongoDB
- Download MongoDB Community Edition:  
  [https://www.mongodb.com/try/download/community](https://www.mongodb.com/try/download/community)

- Install MongoDB (default path:  
  `C:\Program Files\MongoDB\Server\4.2`)

- During installation, ensure that **MongoDB Server** is installed as a Windows Service.

---

### 2. Data Persistence Path (Important)
By default, MongoDB stores data in:

```

C:\Program Files\MongoDB\Server\4.2\data\db

```

⚠️ If you want **long-term persistent data**, it is recommended to change the data path to a separate drive like `D:\`, `E:\`, or `F:\`.

Example recommended path:

```

D:\MKWS\_MERN\_StockManager\Data
D:\MKWS\_MERN\_StockManager\Logs

```

---

### 3. Setup Custom MongoDB Path

1. **Create folders manually** (or let backend auto-create):
```

D:\MKWS\_MERN\_StockManager\Data
D:\MKWS\_MERN\_StockManager\Logs

```

2. **Edit MongoDB config file**  
Open:
```

C:\Program Files\MongoDB\Server\4.2\bin\mongod.cfg

````

Replace with:

systemLog:
  destination: file
  path: D:\MKWS_MERN_StockManager\Logs\mongod.log
  logAppend: true

storage:
  dbPath: D:\MKWS_MERN_StockManager\Data
  journal:
    enabled: true

net:
  bindIp: 127.0.0.1
  port: 27017
````

3. **Reinstall MongoDB Service**

   Open Command Prompt (as Administrator):

   ```bash
   sc stop MongoDB
   sc delete MongoDB

   cd "C:\Program Files\MongoDB\Server\4.2\bin"
   mongod --config "C:\Program Files\MongoDB\Server\4.2\bin\mongod.cfg" --install --serviceName "MongoDB"
   net start MongoDB
   ```

4. **Verify in MongoDB Compass**
   Connect to:

   ```
   mongodb://localhost:27017
   ```

---

### 4. .env Configuration

In the project root `.env` file, update:

```env
PORT=4000
MONGO_URI=mongodb://localhost:27017/mkws_inventory
JWT_SECRET=replace_with_strong_secret
DATA_DIR=D:\MKWS_MERN_StockManager\Data
LOG_DIR=D:\MKWS_MERN_StockManager\Logs
```

---

✅ Now MongoDB will always store data in your specified drive (`D:/E:/F:` etc.) and survive even after reinstalling MongoDB or Windows updates.

```


## 📂 Project Structure

root
├── .git                        # Git repo metadata (commits, branches)
├── .gitignore                  # Ignore files for Git (node_modules, dist, etc.)
├── client                      # React frontend source code
│   ├── .env                    # Frontend environment variables (API URL)
│   ├── .gitignore              # Git ignore rules for frontend
│   ├── CHANGELOG.md            # Track changes/version history
│   ├── index.html              # Entry HTML file for dev (Vite serves this)
│   ├── jsconfig.json           # Path/alias configuration for JS imports
│   ├── LICENSE                 # License file for project usage
│   ├── node_modules            # Installed frontend dependencies
│   ├── package-lock.json       # Auto-generated dependency tree lock
│   ├── package.json            # Frontend project config & dependencies
│   ├── postcss.config.cjs      # PostCSS config (used by Tailwind)
│   ├── prettier.config.js      # Prettier config (code formatting)
│   ├── public                  # Public static assets (copied as-is in build)
│   │   ├── css/tailwind.css    # Raw Tailwind CSS file
│   │   └── img/                # Static images (logos, icons, backgrounds)
│   ├── src                     # Main React source code
│   │   ├── api/api.js          # Axios API instance
│   │   ├── App.jsx             # Root React component
│   │   ├── components/common   # Reusable small UI components
│   │   ├── configs             # Global configs (charts, constants)
│   │   ├── context             # React Context (global providers)
│   │   ├── data                # Dummy data for charts/tables
│   │   ├── layouts             # Layouts (auth, dashboard, wrapper)
│   │   ├── main.jsx            # Entry file, renders React app
│   │   ├── pages               # All main pages/screens
│   │   │   ├── auth            # Sign-in, sign-up pages
│   │   │   ├── dashboard       # Dashboard related pages
│   │   │   ├── low-stock       # Low stock alerts UI
│   │   │   ├── products        # Product CRUD UI
│   │   │   ├── stock           # Stock management components
│   │   │   └── transactions    # Transaction list/detail UI
│   │   ├── redux               # Redux Toolkit slices & store
│   │   ├── routes              # ProtectedRoute wrapper
│   │   ├── routes.jsx          # App routing configuration
│   │   ├── theme               # Theme colors, CSS, theme switcher
│   │   └── widgets             # Cards, charts, navbar, sidenav etc.
│   ├── tailwind.config.cjs     # Tailwind CSS config file
│   └── vite.config.js          # Vite bundler configuration
├── Folder stucture .tex        # Documentation for folder structure
├── readme.md                   # Project documentation
└── server                      # Node.js/Express backend
    ├── .env                    # Backend environment variables
    ├── .gitignore              # Git ignore rules for backend
    ├── config/db.js            # MongoDB connection setup
    ├── controllers             # Business logic (API handlers)
    │   ├── productController.js# Product CRUD + transaction logic
    │   └── userController.js   # User auth, profile, login/signup
    ├── dist                    # Compiled backend (build output)
    │   ├── .env                # Env copy for build
    │   │   ├── .env
    │   │   └── server.exe
    │   └── server.exe          # Compiled backend executable (production run)
    ├── middleware              # Express middlewares
    │   ├── authMiddleware.js   # JWT auth verification
    │   └── errorMiddleware.js  # Error handling middleware
    ├── models                  # MongoDB Mongoose schemas
    │   ├── Product.js          # Product model with transactions
    │   └── User.js             # User model with password hashing
    ├── node_modules            # Installed backend dependencies
    ├── package-lock.json       # Backend dependency tree lock
    ├── package.json            # Backend project config & dependencies
    ├── routes                  # Express routes
    │   ├── productRoutes.js    # Routes for product CRUD & transactions
    │   └── userRoutes.js       # Routes for authentication & profile
    ├── server.js               # Express app entry point
    └── utils/generateToken.js  # JWT token generator helper

```

---

## 🔑 Environment Variables

### Backend (`server/.env`)

```env
PORT=4000
MONGO_URI=mongodb://localhost:27017/mkws_inventory
JWT_SECRET=replace_with_strong_secret
```

### Frontend (`client/.env`)

```env
VITE_API_URL=http://localhost:4000/api
```

---

## 🛠 API Endpoints

### User Routes (`/api/users`)

| Method | Endpoint    | Description                             |
| ------ | ----------- | --------------------------------------- |
| POST   | `/register` | Create new user (name, email, password) |
| POST   | `/login`    | Login user → returns JWT token          |
| GET    | `/profile`  | Get current user info (JWT required)    |

---

### Product Routes (`/api/products`)

| Method | Endpoint       | Description                      |
| ------ | -------------- | -------------------------------- |
| POST   | `/product`     | ➕ Create new product (protected) |
| GET    | `/products`    | 📦 Get all products              |
| GET    | `/product/:id` | 🔎 Get single product by ID      |
| PUT    | `/product/:id` | ✏️ Update product (protected)    |
| DELETE | `/product/:id` | 🗑 Delete product (protected)    |

---

### Stock Transaction Routes

| Method | Endpoint                                         | Description                        |
| ------ | ------------------------------------------------ | ---------------------------------- |
| POST   | `/product/:id/in`                                | ➕ Add stock (In) for product       |
| POST   | `/product/:id/out`                               | ➖ Remove stock (Out) for product   |
| PUT    | `/product/:productId/transaction/:transactionId` | ✏️ Update transaction (by product) |
| DELETE | `/product/:productId/transaction/:transactionId` | 🗑 Delete transaction (by product) |
| PUT    | `/transaction/:transactionId`                    | ✏️ Update transaction **by ID**    |
| DELETE | `/transaction/:transactionId`                    | 🗑 Delete transaction **by ID**    |

> All protected routes require header:
> `Authorization: Bearer <JWT_TOKEN>`

---

### Example API Calls

#### Delete Transaction by ID

```bash
curl -X DELETE http://localhost:4000/api/products/transaction/<TRANSACTION_ID> \
-H "Authorization: Bearer <TOKEN>"
```

#### Update Transaction by ID

```bash
curl -X PUT http://localhost:4000/api/products/transaction/<TRANSACTION_ID> \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <TOKEN>" \
-d '{"type":"OUT","amount":5,"remark":"Correction"}'
```

---

## ⚡ Frontend Setup (Development)

```bash
cd client
npm install
npm run dev
```

Runs frontend at `http://localhost:5173`

---

## 🚀 Backend Setup (Development)

```bash
cd server
npm install
npm run dev
```

Runs backend at `http://localhost:4000`

---

## 📦 Production Build

1. **Build Frontend (React → dist folder):**

   ```bash
   cd client
   npm run build
   ```

2. **Build Backend (Node → EXE):**

   ```bash
   cd server
   npm run build
   ```

   This generates:

   ```
   server/dist/server.exe
   ```

3. Now you can run backend + serve frontend with:

   ```bash
   server/dist/server.exe
   ```

---

## 🖥 Run Server as Windows Service (Auto Start at Boot)

We’ll use **NSSM (Non-Sucking Service Manager)** to install `server.exe` as a service.

1. **Download NSSM:**
   👉 [https://nssm.cc/download](https://nssm.cc/download)

2. Extract and copy `nssm.exe` → `C:\Windows\System32`

3. Open **Command Prompt as Administrator** and run:

   ```cmd
   nssm install MKWS-Server
   ```

   Fill in:

   * **Path:**
     `C:\Users\M FAHAD\Desktop\final\server\dist\server.exe`
   * **Startup directory:**
     `C:\Users\M FAHAD\Desktop\final\server\dist`

   Click **Install Service**.

4. Start the service:

   ```cmd
   nssm start MKWS-Server
   ```

5. Service will now **auto-start** whenever Windows boots.

---

## 🖱 Desktop Shortcut for Dashboard

For easy access, create a shortcut on Desktop:

1. Right-click Desktop → **New → Shortcut**
2. Location:

   ```
   http://localhost:4000
   ```
3. Name it: `MKWS Inventory Dashboard`

Now backend will already be running in the background (as service), and users can simply double-click this shortcut to open the dashboard in their browser.

---

✅ With this setup:

* Backend runs silently as a service (no console window).
* React frontend build is served from the same `server.exe`.
* User only needs Desktop shortcut → opens `http://localhost:4000`.

---