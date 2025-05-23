
# 📊 Grafana Cheat Sheet

## 📚 Key Concepts

| Term | Description |
|------|-------------|
| **Datasource** | Connection to a database or metric provider (e.g., Prometheus, InfluxDB, MySQL). |
| **Dashboard** | A collection of panels organized to display data visually. |
| **Panel** | A single visualization (e.g., graph, gauge, table) within a dashboard. |
| **Query Editor** | UI for writing and testing data queries per panel, varies by datasource. |
| **Variables** | Dynamic values that can be reused across panels and queries. |
| **Annotations** | Visual markers to add context to graphs (e.g., deployments). |
| **Alerting** | Set thresholds to trigger alerts via email, Slack, etc. |
| **Templating** | Use variables to create interactive and reusable dashboards. |

## 🖼️ Creating a Dashboard

### ➕ Create New Dashboard
1. Go to **Dashboard** → **New** → **New Dashboard**.
2. Click **Add a new panel**.

## 📊 Creating a Panel

### ➕ Add Panel
1. Choose **Add Panel**.
2. Select a **Visualization Type**: Graph, Gauge, Table, Bar Gauge, Heatmap, etc.
3. Configure the **Query** (based on your datasource):
   - For **Prometheus**:
     ```promql
     rate(http_requests_total[5m])
     ```
   - For **MySQL**:
     ```sql
     SELECT time, value FROM metrics WHERE $__timeFilter(time)
     ```
4. Customize visualization:
   - **Title**
   - **Axis labels**
   - **Legend**
   - **Thresholds**
   - **Units** (ms, %, etc.)
5. Click **Apply** to add it to the dashboard.

## 🧠 Using Variables

### ➕ Create a Variable
1. Go to **Dashboard Settings** → **Variables** → **New**.
2. Give a name (e.g., `server`).
3. Choose **Type**: Query, Custom, Constant, etc.
4. Example (for Prometheus):
   ```promql
   label_values(instance)
   ```

### 🧠 Use in Query
```promql
rate(http_requests_total{instance="$server"}[5m])
```

## 🔔 Setting Up Alerts

1. Open a panel → click **Alert** tab.
2. Set:
   - **Conditions**: e.g., `WHEN avg() OF query(A, 5m, now) IS ABOVE 100`
   - **Evaluate every**: 1m, 5m, etc.
3. Add **Notification channel** (Slack, Email, Webhook).
4. Save panel to enable alerts.

## 🗂 Useful Tips

- **Time Ranges**: Use top-right time picker to zoom in/out or pick relative ranges (`Last 5 minutes`, `Last 7 days`).
- **Links**: Use **Dashboard Links** and **Panel Links** to navigate between dashboards.
- **JSON Model**: Dashboards can be exported/imported via JSON from the settings menu.

## 🧪 CLI Commands

```bash
grafana-cli plugins install <plugin-id>    # Install a plugin
grafana-cli admin reset-admin-password <new-password>
```

## 🔒 Permissions

- **Folder-level access control**
- Users/Teams can have:
  - Viewer
  - Editor
  - Admin rights
