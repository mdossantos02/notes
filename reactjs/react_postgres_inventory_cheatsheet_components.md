
# 🧰 React + PostgreSQL Inventory App Starter Cheat Sheet

This cheat sheet guides you to build a full-stack inventory application using React.js for the frontend, Express/Node.js for the backend, and PostgreSQL as the database.

---

## 📁 Project Structure

```
inventory-app/
├── backend/
│   ├── db/
│   │   └── index.js
│   ├── routes/
│   │   └── items.js
│   ├── .env
│   ├── server.js
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   └── App.jsx
│   ├── public/
│   ├── .env
│   └── package.json
└── README.md
```

---

## 🧱 Backend Setup (Node.js + Express + PostgreSQL)

### 1. Initialize Backend

```bash
mkdir backend && cd backend
npm init -y
npm install express pg cors dotenv
```

### 2. Create `.env` in `backend/`

```env
PORT=5000
PG_USER=youruser
PG_HOST=localhost
PG_DATABASE=inventory
PG_PASSWORD=yourpassword
PG_PORT=5432
```

### 3. `db/index.js`

```js
const { Pool } = require("pg");
require("dotenv").config();

const pool = new Pool({
  user: process.env.PG_USER,
  host: process.env.PG_HOST,
  database: process.env.PG_DATABASE,
  password: process.env.PG_PASSWORD,
  port: process.env.PG_PORT,
});

module.exports = pool;
```

### 4. `server.js`

```js
const express = require("express");
const cors = require("cors");
const app = express();
require("dotenv").config();
const itemRoutes = require("./routes/items");

app.use(cors());
app.use(express.json());
app.use("/api/items", itemRoutes);

app.listen(process.env.PORT, () =>
  console.log(`Server running on port ${process.env.PORT}`)
);
```

### 5. `routes/items.js`

```js
const express = require("express");
const router = express.Router();
const pool = require("../db");

router.get("/", async (req, res) => {
  const items = await pool.query("SELECT * FROM items");
  res.json(items.rows);
});

router.post("/", async (req, res) => {
  const { name, quantity } = req.body;
  const newItem = await pool.query(
    "INSERT INTO items (name, quantity) VALUES ($1, $2) RETURNING *",
    [name, quantity]
  );
  res.json(newItem.rows[0]);
});

module.exports = router;
```

### 6. PostgreSQL Table

```sql
CREATE TABLE items (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  quantity INTEGER
);
```

---

## 🎨 Frontend Setup (React.js)

### 1. Create App

```bash
npx create-react-app frontend
cd frontend
npm install axios react-router-dom
```

### 2. `.env` in `frontend/`

```env
REACT_APP_API_URL=http://localhost:5000/api
```

### 3. `src/App.jsx`

```jsx
import React, { useEffect, useState } from "react";
import axios from "axios";

const App = () => {
  const [items, setItems] = useState([]);
  const [form, setForm] = useState({ name: "", quantity: "" });

  useEffect(() => {
    axios.get(`${process.env.REACT_APP_API_URL}/items`)
      .then(res => setItems(res.data));
  }, []);

  const handleSubmit = async (e) => {
    e.preventDefault();
    await axios.post(`${process.env.REACT_APP_API_URL}/items`, form);
    const res = await axios.get(`${process.env.REACT_APP_API_URL}/items`);
    setItems(res.data);
    setForm({ name: "", quantity: "" });
  };

  return (
    <div>
      <h1>Inventory</h1>
      <form onSubmit={handleSubmit}>
        <input placeholder="Name" value={form.name} onChange={e => setForm({...form, name: e.target.value})} />
        <input placeholder="Quantity" type="number" value={form.quantity} onChange={e => setForm({...form, quantity: e.target.value})} />
        <button type="submit">Add</button>
      </form>
      <ul>
        {items.map(item => <li key={item.id}>{item.name}: {item.quantity}</li>)}
      </ul>
    </div>
  );
};

export default App;
```

---

## 🚀 Run the App

### Backend:

```bash
cd backend
node server.js
```

### Frontend:

```bash
cd frontend
npm start
```

---

## 🛠 Step-by-Step: Installing Node.js and Setting Up in VS Code

### 🧩 Step 1: Install Node.js

1. Go to the [Node.js download page](https://nodejs.org/)
2. Download the **LTS version** for your OS.
3. Run the installer and follow the prompts (accept defaults).
4. Verify installation:
   ```bash
   node -v
   npm -v
   ```

### 🧩 Step 2: Set Up VS Code

1. Download and install [Visual Studio Code](https://code.visualstudio.com/)
2. Open VS Code and install the following extensions:
   - **ESLint** (for JavaScript/React linting)
   - **Prettier** (code formatting)
   - **DotENV** (for highlighting `.env` files)

### 🧩 Step 3: Initialize Backend

1. Open a terminal in VS Code.
2. Run the following to set up backend:
   ```bash
   mkdir backend
   cd backend
   npm init -y
   npm install express pg cors dotenv
   ```

### 🧩 Step 4: Initialize Frontend

1. Open a new terminal tab in VS Code.
2. Run the following:
   ```bash
   npx create-react-app frontend
   cd frontend
   npm install axios react-router-dom
   ```

### 🧩 Step 5: Run the Full Stack App

- In one terminal, run the backend:
  ```bash
  cd backend
  node server.js
  ```

- In another terminal, run the frontend:
  ```bash
  cd frontend
  npm start
  ```

---

With these steps, you’ll be able to code, run, and debug both the frontend and backend inside Visual Studio Code.

---

## 🧩 React Components: Creating and Compiling

### 📦 Component Basics

A React component is a reusable piece of UI. You can create either a function component or a class component (function is preferred in modern React).

### 🛠 Example: Function Component

Create a new file in `src/components/ItemList.jsx`:

```jsx
import React from "react";

const ItemList = ({ items }) => (
  <ul>
    {items.map(item => (
      <li key={item.id}>{item.name}: {item.quantity}</li>
    ))}
  </ul>
);

export default ItemList;
```

### 🧱 Using the Component in App

In `App.jsx`:

```jsx
import ItemList from "./components/ItemList";

// Inside return()
<ItemList items={items} />
```

### ⚙️ Compilation & Build

React uses **Webpack** and **Babel** behind the scenes (included with Create React App) to:

- Compile JSX to JavaScript
- Bundle JavaScript/CSS assets
- Serve optimized builds in production

### 📦 Development Build

To run a local dev server with hot-reloading:

```bash
npm start
```

### 📦 Production Build

To compile and optimize your app for production:

```bash
npm run build
```

This creates a `build/` folder with static assets that can be deployed.

### 🧪 Testing Components (Optional)

Install React Testing Library for unit tests:

```bash
npm install --save-dev @testing-library/react
```

Create a test:

```jsx
// ItemList.test.js
import { render, screen } from "@testing-library/react";
import ItemList from "./ItemList";

test("renders item list", () => {
  render(<ItemList items={[{ id: 1, name: "Test", quantity: 2 }]} />);
  expect(screen.getByText("Test: 2")).toBeInTheDocument();
});
```

Run tests with:

```bash
npm test
```
