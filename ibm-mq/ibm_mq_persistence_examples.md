
# IBM MQ: Message Persistence – Code Examples and Test Scenarios

This guide provides examples and test cases to better understand how persistent and non-persistent messaging works in IBM MQ.

---

## 🧪 MQSC Queue Setup

### Create Queues with Different Default Persistence

```bash
DEFINE QLOCAL('PERSIST.QUEUE') DEFPSIST(YES)
DEFINE QLOCAL('NOPERSIST.QUEUE') DEFPSIST(NO)
```

---

## 🖥️ Example: Sending Messages with amqsput

### A. Using Default Persistence from Queue
```bash
amqsput PERSIST.QUEUE QM1
Hello Persistent
<Ctrl+D>
```

```bash
amqsput NOPERSIST.QUEUE QM1
Hello Non-Persistent
<Ctrl+D>
```

---

## 👨‍💻 Example: Java Code Snippet

```java
MQMessage message = new MQMessage();
message.writeString("Hello MQ");

// Set explicit persistence
message.persistence = MQC.MQPER_PERSISTENT;

MQPutMessageOptions pmo = new MQPutMessageOptions();
queue.put(message, pmo);
```

Replace `MQPER_PERSISTENT` with `MQPER_NOT_PERSISTENT` to test non-persistent behavior.

---

## 🧪 Test Scenario

1. **Send a message to each queue**.
2. **Stop the queue manager**:
   ```bash
   endmqm -i QM1
   ```
3. **Start it again**:
   ```bash
   strmqm QM1
   ```
4. **Retrieve messages**:
   ```bash
   amqsget PERSIST.QUEUE QM1   # Message should be present
   amqsget NOPERSIST.QUEUE QM1 # Message likely gone
   ```

---

## 📈 Expected Results

| Queue            | Message Visible After Restart? | Explanation                      |
|------------------|-------------------------------|----------------------------------|
| PERSIST.QUEUE    | ✅ Yes                         | Stored on disk                   |
| NOPERSIST.QUEUE  | ❌ No                          | Only in memory (not durable)     |

---

## 🔍 Diagnostic Tools

- `dmpmqlog`: Inspect message logs
- `strmqtrc / endmqtrc`: Start/stop tracing
- `amqsbcg <QUEUE> <QMGR>`: Browse queue contents with metadata

---

## ✅ Summary

Use persistent messages when delivery guarantees are required. Use non-persistent messages for faster, best-effort delivery where occasional loss is acceptable.

---

Need examples in Python or .NET as well?
