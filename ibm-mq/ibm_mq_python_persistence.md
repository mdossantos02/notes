
# IBM MQ: Python Code Examples for Message Persistence

This guide demonstrates how to send persistent and non-persistent messages using Python and `pymqi`.

---

## 📦 Prerequisites

Install `pymqi`:
```bash
pip install pymqi
```

Ensure IBM MQ client libraries are installed and available on your system.

---

## 🧰 Setup Parameters

```python
import pymqi

queue_manager = 'QM1'
channel = 'DEV.APP.SVRCONN'
host = 'localhost'
port = '1414'
conn_info = f'{host}({port})'
queue_name = 'PERSIST.QUEUE'

user = 'app'
password = 'pass'
```

---

## 📨 Send a Persistent Message

```python
qmgr = pymqi.connect(queue_manager, channel, conn_info, user, password)
queue = pymqi.Queue(qmgr, queue_name)

message = b"Hello Persistent"
queue.put(message, pymqi.MQPMO(), persistence=pymqi.CMQC.MQPER_PERSISTENT)

queue.close()
qmgr.disconnect()
```

---

## 📨 Send a Non-Persistent Message

```python
qmgr = pymqi.connect(queue_manager, channel, conn_info, user, password)
queue = pymqi.Queue(qmgr, queue_name)

message = b"Hello Non-Persistent"
queue.put(message, pymqi.MQPMO(), persistence=pymqi.CMQC.MQPER_NOT_PERSISTENT)

queue.close()
qmgr.disconnect()
```

---

## 🧪 Test After Queue Manager Restart

1. Run the script to send each message.
2. Restart the queue manager:
   ```bash
   endmqm -i QM1
   strmqm QM1
   ```
3. Use `amqsget` or another consumer to verify which messages remain.

---

## ✅ Summary

- Use `MQPER_PERSISTENT` for durability across restarts.
- Use `MQPER_NOT_PERSISTENT` for speed when loss is acceptable.

---


