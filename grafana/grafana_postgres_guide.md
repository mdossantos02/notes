
# 📈 Connect Grafana to PostgreSQL and Visualize a Report

## 🛠️ Step-by-Step Guide

---

### ✅ 1. Prepare Your PostgreSQL Database

Ensure your PostgreSQL:
- Is running and accessible from the machine Grafana is installed on.
- Accepts connections from Grafana's IP address.
- Has the necessary user and permissions to run SELECT queries.

```sql
CREATE USER grafana_user WITH PASSWORD 'yourpassword';
GRANT CONNECT ON DATABASE your_database TO grafana_user;
GRANT USAGE ON SCHEMA public TO grafana_user;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO grafana_user;
```

---

### ✅ 2. Log into Grafana

- Open your browser and go to: `http://<your-server-ip>:3000`
- Log in (default: `admin` / `admin`).

---

### ✅ 3. Add PostgreSQL as a Data Source

1. Click the **gear icon** (⚙️) on the left sidebar → **Data Sources**.
2. Click **Add data source**.
3. Choose **PostgreSQL** from the list.

---

### ✅ 4. Configure the PostgreSQL Data Source

Fill in these fields:

| Field | Example |
|-------|---------|
| **Name** | `Postgres-Metrics` |
| **Host** | `localhost:5432` (or IP:port) |
| **Database** | `your_database` |
| **User** | `grafana_user` |
| **Password** | `yourpassword` |
| **SSL Mode** | `disable` (or `require` if using SSL) |
| **Version** | Auto-detect or manually set (e.g., `14`) |

Click **Save & Test** to confirm connection.

---

### ✅ 5. Create a Dashboard

1. On the sidebar, click **Dashboard** → **New** → **New Dashboard**.
2. Click **Add a new panel**.

---

### ✅ 6. Write a PostgreSQL Query

Use SQL in the query editor. For example:

```sql
SELECT
  time_column AS "time",
  value_column AS "value",
  label_column AS "metric"
FROM your_table
WHERE $__timeFilter(time_column)
```

> 🔍 Tip: Grafana uses `$__timeFilter(column)` to inject the dashboard’s time range into your query.

---

### ✅ 7. Choose a Visualization

- Options: **Time series**, **Table**, **Bar chart**, etc.
- Choose depending on what you're trying to report (e.g., time series for trends, table for tabular data).

Customize:
- **Axes**, **Legends**, **Colors**, **Thresholds**, etc.

Click **Apply**.

---

### ✅ 8. Save Your Dashboard

- Click the **disk icon** (💾) → Name your dashboard → **Save**.

---

### 🧠 Extras

- Use **Variables** to allow users to filter data (e.g., by region or department).
- Use **Annotations** for marking events (e.g., deployments).
- Create **Alerts** on panels if needed.
