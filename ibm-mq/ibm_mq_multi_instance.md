
# IBM MQ: Multi-Instance Queue Managers

Multi-instance queue managers provide **high availability (HA)** by running multiple instances of the same queue manager on different hosts, using shared storage.

---

## 🧩 Key Concepts

- **Active Instance**: The currently running queue manager.
- **Standby Instance**: Waits and monitors the shared storage.
- **Shared Storage**: Both instances access the same logs and message data.
- Only one instance runs at a time.

---

## 🏗️ Prerequisites

- Two or more servers with IBM MQ installed.
- Shared file system (e.g., NFS) accessible by all instances.
- Identical MQ installation paths on each host.
- Same user ID and group for `mqm` across servers.

---

## 📁 Directory Structure Example

```plaintext
/mqshared/qmgrs/QM1       # Queue manager config and data
/mqshared/log/QM1         # Log files
```

Mount this shared directory on all participating servers at the same path.

---

## 🛠️ Creating a Multi-Instance Queue Manager

On one host (e.g., HostA):

```bash
crtmqm -fs /mqshared/log -md /mqshared/qmgrs QM1
```

Start it as the **active** instance:

```bash
strmqm QM1
```

On the second host (e.g., HostB), start the **standby**:

```bash
strmqm -x QM1
```

---

## 🔁 How Failover Works

1. Active instance fails or crashes.
2. Standby detects loss of file lock.
3. Standby automatically takes over.

To monitor the state:

```bash
dspmq
```

Example output:

```
QMNAME(QM1) STATUS(Running) INST(Active) ...
QMNAME(QM1) STATUS(Running) INST(Standby) ...
```

---

## 🔒 Permissions and Configuration

- Ensure `mqm` has read/write access to the shared storage.
- Use consistent user/group IDs across hosts.
- Check NFS options: `nolock`, `hard`, and `timeo`.

---

## 🚨 Considerations

- Not suitable for cloud-native environments.
- Shared storage is a **single point of failure**.
- Useful for **on-premise HA** when simple failover is sufficient.

---

## ✅ Summary

| Component         | Description                                 |
|------------------|---------------------------------------------|
| Active Instance  | Runs the queue manager                      |
| Standby Instance | Monitors and takes over if active fails     |
| Shared Storage   | Common location for data/logs               |
| NFS/Cluster FS   | Required for shared file system             |

---


