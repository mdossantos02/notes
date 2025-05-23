
# Essential Linux Commands

This document lists the most important Linux commands for everyday use, including editing files, installing programs, managing files, and understanding where to install things.

---

## 📝 File Editing

### Using `nano` (simple terminal editor)
```bash
nano filename
```
- Use `CTRL + O` to save, `CTRL + X` to exit.

### Using `vim` (advanced terminal editor)
```bash
vim filename
```
- `i` to enter insert mode
- `ESC` to exit insert mode
- `:w` to save, `:q` to quit, `:wq` to save and quit

### Using `cat`, `echo`, and `>` for quick edits
```bash
cat > filename  # Type content, press CTRL+D to save
echo "text" > filename  # Overwrites
echo "text" >> filename  # Appends
```

---

## 📦 Installing Programs

### Debian/Ubuntu (APT)
```bash
sudo apt update
sudo apt install packagename
```

### Red Hat/CentOS/Fedora (YUM or DNF)
```bash
sudo yum install packagename
# or
sudo dnf install packagename
```

### Arch Linux (Pacman)
```bash
sudo pacman -S packagename
```

### Snap (Universal package manager)
```bash
sudo snap install packagename
```

### Flatpak
```bash
flatpak install flathub packagename
```

---

## 📂 Where to Install Things

| Location               | Purpose                                           |
|------------------------|---------------------------------------------------|
| `/usr/bin`             | Standard location for user commands               |
| `/usr/local/bin`       | Locally compiled software                         |
| `/opt`                 | Optional, large, or third-party software          |
| `~/bin`                | User's personal scripts/executables               |
| `/etc`                 | System configuration files                        |

To make your local binaries executable system-wide:
```bash
export PATH=$PATH:$HOME/bin
```

---

## 📁 File and Directory Management

### Basic Commands
```bash
ls -l        # List files with details
cd /path     # Change directory
pwd          # Print working directory
mkdir name   # Make new directory
touch file   # Create empty file
rm file      # Remove file
rm -r folder # Remove directory and contents
cp a b       # Copy file a to b
mv a b       # Move/rename file a to b
```

---

## 🔍 Searching and Finding

```bash
find /path -name filename       # Find file by name
grep "text" file                # Search text in file
grep -r "text" /path            # Recursive search
locate filename                 # Fast search using index (run `updatedb` first)
```

---

## 🔧 System Monitoring and Management

```bash
top              # Real-time system processes
htop             # Better version of top (may need install)
df -h            # Disk usage
du -sh *         # Directory sizes
free -h          # Memory usage
uptime           # System uptime
ps aux | grep x  # Process search
kill PID         # Kill process
```

---

## 🔐 Permissions and Ownership

```bash
chmod +x script.sh     # Make file executable
chmod 755 file         # Common permissions for scripts
chown user:group file  # Change ownership
```

---

## 🔄 Network

```bash
ping example.com       # Check network connection
curl example.com       # Get content from URL
wget url               # Download file from URL
ip a                  # Show IP addresses
```

---

## 💡 Useful Shortcuts

```bash
!!         # Repeat last command
!abc       # Repeat last command starting with abc
CTRL+C     # Cancel current command
CTRL+R     # Search through command history
TAB        # Auto-complete command or filename
```

---

## 📜 Miscellaneous

```bash
man command         # Manual page for a command
which command       # Path of command binary
alias ll='ls -la'   # Create command alias
history             # Show command history
```

---

## 🔁 Script Execution

```bash
./script.sh           # Run a script
bash script.sh        # Run with bash
sh script.sh          # Run with sh
```

> Make sure the script has execute permission: `chmod +x script.sh`

---

## 📁 Filesystem Overview (Common Directories)

| Directory      | Purpose                          |
|----------------|----------------------------------|
| `/bin`         | Essential binary executables     |
| `/sbin`        | System binaries                  |
| `/etc`         | Configuration files              |
| `/home`        | User home directories            |
| `/lib`, `/lib64` | Essential libraries            |
| `/var`         | Variable data (logs, spool)      |
| `/tmp`         | Temporary files                  |
| `/usr`         | Secondary hierarchy (apps, docs) |
| `/opt`         | Optional add-on applications     |

---

## 📚 Learn More

- `man command` – the built-in manual
- `tldr command` – simplified help pages (install with `npm install -g tldr`)
- [https://explainshell.com](https://explainshell.com) – for breaking down commands


---

## 🔐 SSH Setup and Key Authentication

### 🛠️ Installing OpenSSH Server (Debian/Ubuntu)

```bash
sudo apt update
sudo apt install openssh-server
sudo systemctl start ssh
sudo systemctl enable ssh
```

### 🔓 Allow SSH Through Firewall (UFW)

```bash
sudo ufw allow ssh
sudo ufw enable
```

### ✅ Generate SSH Key Pair (on the client)

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

- Private key: `~/.ssh/id_rsa`
- Public key: `~/.ssh/id_rsa.pub`

### 📤 Copy the Public Key to the Server

```bash
ssh-copy-id your_user@server_ip
```

Or manually copy `~/.ssh/id_rsa.pub` contents into the server’s:

```
~/.ssh/authorized_keys
```

### 🔐 Permissions (on the server)

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

### 🚀 Connect to Server Using Key

```bash
ssh your_user@server_ip
```

Or, if using a custom key file:

```bash
ssh -i ~/.ssh/your_key_file your_user@server_ip
```

