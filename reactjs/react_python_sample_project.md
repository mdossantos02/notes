
# 🧩 Sample React + Python (Flask) Full-Stack App

This is a simple full-stack application where a React frontend communicates with a Python Flask backend.

---

## 📁 Project Structure

```
react-python-app/
├── backend/
│   ├── app.py
│   ├── requirements.txt
│   └── .venv/ (optional)
└── frontend/
    ├── src/
    │   ├── App.jsx
    │   └── index.js
    ├── public/
    └── package.json
```

---

## 🧱 Backend Setup (Python + Flask)

### 1. Create Backend Folder

```bash
mkdir backend && cd backend
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install flask flask-cors
pip freeze > requirements.txt
```

### 2. `app.py`

```python
from flask import Flask, jsonify, request
from flask_cors import CORS

app = Flask(__name__)
CORS(app)

@app.route("/api/items", methods=["GET"])
def get_items():
    return jsonify([
        {"id": 1, "name": "Widget", "quantity": 10},
        {"id": 2, "name": "Gadget", "quantity": 5}
    ])

@app.route("/api/items", methods=["POST"])
def add_item():
    data = request.get_json()
    return jsonify({"message": "Item added", "item": data})

if __name__ == "__main__":
    app.run(debug=True, port=5000)
```

---

## 🎨 Frontend Setup (React)

### 1. Create React App

```bash
npx create-react-app frontend
cd frontend
npm install axios
```

### 2. `src/App.jsx`

```jsx
import React, { useEffect, useState } from "react";
import axios from "axios";

const App = () => {
  const [items, setItems] = useState([]);
  const [form, setForm] = useState({ name: "", quantity: "" });

  useEffect(() => {
    axios.get("http://localhost:5000/api/items")
      .then(res => setItems(res.data));
  }, []);

  const handleSubmit = async (e) => {
    e.preventDefault();
    await axios.post("http://localhost:5000/api/items", form);
    const res = await axios.get("http://localhost:5000/api/items");
    setItems(res.data);
    setForm({ name: "", quantity: "" });
  };

  return (
    <div className="container mt-4">
      <h1>Inventory</h1>
      <form onSubmit={handleSubmit}>
        <input
          placeholder="Name"
          value={form.name}
          onChange={(e) => setForm({ ...form, name: e.target.value })}
        />
        <input
          placeholder="Quantity"
          type="number"
          value={form.quantity}
          onChange={(e) => setForm({ ...form, quantity: e.target.value })}
        />
        <button type="submit">Add</button>
      </form>
      <ul>
        {items.map((item) => (
          <li key={item.id}>{item.name}: {item.quantity}</li>
        ))}
      </ul>
    </div>
  );
};

export default App;
```

---

## 🚀 Run the App

### Backend (Python Flask)

```bash
cd backend
source .venv/bin/activate  # Windows: .venv\Scripts\activate
python app.py
```

### Frontend (React)

```bash
cd frontend
npm start
```

---

## ✅ Notes

- Ensure CORS is enabled in Flask to avoid browser restrictions.
- Update the `localhost` URL if you're deploying or running on different ports or machines.
