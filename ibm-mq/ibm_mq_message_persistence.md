
# IBM MQ: In-Depth Guide to Message Persistence

Message persistence is a key feature of IBM MQ that ensures **reliable delivery and durability** of messages—even in the event of crashes, restarts, or network failures.

---

## 🔐 What Is Message Persistence?

Persistence defines whether a message survives:

- **Queue manager restarts**
- **System crashes**
- **Power failures**

---

## 🧱 Persistent vs Non-Persistent Messages

| Type             | Stored on Disk | Survives Restart | Delivery Guarantee |
|------------------|----------------|------------------|--------------------|
| Persistent       | ✅             | ✅               | Exactly-once       |
| Non-Persistent   | ❌ (in memory) | ❌               | At-most-once       |

---

## 🛠 How to Set Persistence

### A. Application-Level
When sending a message, specify the **persistence flag**:
- `MQPER_PERSISTENT`
- `MQPER_NOT_PERSISTENT`
- `MQPER_PERSISTENCE_AS_Q_DEF`

### B. Queue-Level Default
Set a queue’s default persistence:
```bash
DEFINE QLOCAL('MY.QUEUE') DEFPSIST(YES)
```

---

## 📂 Storage Internals

### 1. **Log Files**
Persistent messages are first written to **transaction logs**:
- Located in `/var/mqm/log/<QMGR_NAME>/active`
- Ensure durability before acknowledging message receipt

### 2. **Queue Files**
Messages are then written to **queue data files** in:
```
/var/mqm/qmgrs/<QMGR_NAME>/queues/
```

---

## 🔄 Transaction Semantics

Persistent messages are:
1. Logged before being placed on the queue.
2. Included in **unit-of-work (UOW)** transactions.
3. Rolled back if a transaction fails.

---

## ⚙️ Log Types

- **Circular Logging** (default)
  - Reuses log space
  - Limited recovery history
- **Linear Logging**
  - Logs are kept until manually archived
  - Required for media recovery

Set in `qm.ini`:
```ini
Log:
  LogType=LINEAR
```

---

## 📦 Performance Considerations

- Persistent messages are **slower** due to disk I/O.
- Use **non-persistent** for high-speed, low-risk data (e.g., monitoring events).
- Use **grouped transactions** to optimize throughput.

---

## 🔍 Monitoring and Debugging

- Use `dmpmqlog` to inspect logs.
- Monitor disk space on log and data directories.
- Check `amqerr01.log` for persistence-related errors.

---

## ✅ Summary

| Feature               | Persistent Msgs       | Non-Persistent Msgs |
|------------------------|------------------------|----------------------|
| Stored on disk        | ✅                     | ❌                   |
| Survive crash/restart | ✅                     | ❌                   |
| Guaranteed delivery   | ✅ (exactly-once)      | ❌ (best effort)     |
| Slower performance    | ✅                     | ❌                   |

---


