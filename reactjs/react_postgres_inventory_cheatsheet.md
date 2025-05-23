
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
