
# Does IBM MQ Store Data?

## ✅ Yes, IBM MQ Stores Data

IBM MQ has a backend storage system to ensure **reliable and durable message delivery**.

---

## 🔧 What IBM MQ Stores

1. **Messages**
   - **Persistent messages**: Written to disk; survive restarts or crashes.
   - **Non-persistent messages**: Stored in memory; faster but volatile.

2. **Queue Definitions and Configurations**
   - Stored in internal system objects and files managed by the queue manager.

3. **Queue Manager State**
   - Tracks queues, message states, IDs, etc.

4. **Transaction Logs**
   - Supports crash recovery using **write-ahead logging**.

---

## 💾 Where IBM MQ Stores Data (Backend)

IBM MQ uses the **local file system** for data persistence.

| Component            | Default Location (Linux/Unix)             | Description                              |
|---------------------|--------------------------------------------|------------------------------------------|
| Queue Manager Data  | `/var/mqm/qmgrs/<QMGR_NAME>`               | Queue and message data                   |
| Logs                | `/var/mqm/log/<QMGR_NAME>`                 | Transaction and recovery logs            |
| Configuration Files | `/var/mqm`                                 | Global MQ configuration files            |

> **Windows Path Example**: `C:\ProgramData\IBM\MQ`

---

## 🧠 Summary

- **IBM MQ does store data**.
- It uses the **file system and logs** as its backend storage.
- It is **not a database**, but offers **durable, ACID-compliant message handling**.

---


