
# ⚡ Sample React + FastAPI Full-Stack App

This is a simple full-stack application where a React frontend communicates with a Python FastAPI backend.

---

## 📁 Project Structure

```
react-fastapi-app/
├── backend/
│   ├── app/
│   │   ├── main.py
│   └── requirements.txt
└── frontend/
    ├── src/
    │   ├── App.jsx
    │   └── index.js
    ├── public/
    └── package.json
```

---

## 🚀 Backend Setup (FastAPI + Uvicorn)

### 1. Create Backend Folder

```bash
mkdir -p backend/app && cd backend
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install fastapi uvicorn[standard] pydantic[dotenv] python-multipart
pip install aiofiles  # For serving static files if needed
pip install fastapi-cors
pip freeze > requirements.txt
```

### 2. `app/main.py`

```python
from fastapi import FastAPI, Request
from fastapi.middleware.cors import CORSMiddleware
from pydantic import BaseModel

app = FastAPI()

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

class Item(BaseModel):
    name: str
    quantity: int

@app.get("/api/items")
async def get_items():
    return [
        {"id": 1, "name": "Widget", "quantity": 10},
        {"id": 2, "name": "Gadget", "quantity": 5}
    ]

@app.post("/api/items")
async def add_item(item: Item):
    return {"message": "Item added", "item": item}
```

### 3. Run FastAPI server

```bash
cd backend
uvicorn app.main:app --reload --port 5000
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

## 📦 Packaging the FastAPI App

### Option 1: Using pip

1. Create a `setup.py` in the backend directory:

```python
from setuptools import setup, find_packages

setup(
    name="inventory_backend",
    version="0.1",
    packages=find_packages(),
    install_requires=open("requirements.txt").read().splitlines(),
)
```

2. Install as a package:

```bash
pip install -e .
```

### Option 2: Docker

1. `backend/Dockerfile`

```dockerfile
FROM python:3.11

WORKDIR /app
COPY ./app /app/app
COPY requirements.txt /app
RUN pip install --no-cache-dir -r requirements.txt

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "5000"]
```

2. Build and run the container:

```bash
docker build -t fastapi-inventory-backend .
docker run -p 5000:5000 fastapi-inventory-backend
```

---

## ✅ Notes

- FastAPI supports async natively, making it very performant.
- Use `.env` and Pydantic settings for configuration management in production.
