
# 🐧 Linux Disk Space & Partitioning Cheatsheet

## 📦 Disk Space and Usage

### `df` - Disk Free
```bash
df -h
```
- Shows disk space on mounted filesystems.
- `-h`: Human-readable (e.g. GB/MB)

### `du` - Disk Usage
```bash
du -sh /path/to/dir
```
- `-s`: Summarize total
- `-h`: Human-readable

To check usage for subdirectories:
```bash
du -h --max-depth=1 /path
```

### `ls -lh` and `ls -lSh`
```bash
ls -lh        # Shows file sizes in current dir
ls -lSh       # Sorts files by size
```

## 💽 Partition and Filesystem Information

### `lsblk` - List Block Devices
```bash
lsblk
lsblk -f      # Shows filesystem types, labels, UUIDs
```

### `fdisk` - Partition Table
```bash
sudo fdisk -l
```
- Lists partitions on all attached drives.

### `blkid` - Block Device Info
```bash
sudo blkid
```
- Shows UUID, filesystem type, labels.

## 🔗 Mount Points

### `mount` - Mounted Filesystems
```bash
mount | column -t
```

### `findmnt` - Structured Mount Tree
```bash
findmnt
```

## 📊 Inode Usage

### `df -i` - Inodes Info
```bash
df -i
```
- Use when disk space is free, but can’t create files.

## 🔍 Interactive Usage Analysis

### `ncdu` - NCurses Disk Usage
```bash
sudo apt install ncdu        # Debian/Ubuntu
sudo yum install ncdu        # RHEL/CentOS
ncdu /
```
- Interactive file browser showing usage.

## 🧠 Summary Table

| Command     | Purpose                          |
|-------------|----------------------------------|
| `df -h`     | Disk space usage (per mount)     |
| `du -sh`    | Space used by folder             |
| `lsblk -f`  | Disks and filesystems            |
| `fdisk -l`  | Partition table overview         |
| `blkid`     | UUID and FS info                 |
| `mount`     | Mounted filesystems              |
| `findmnt`   | Mount tree (structured)          |
| `df -i`     | Inodes usage                     |
| `ncdu`      | Interactive disk usage analyzer  |


## 📁 File Copy and Archive Management

### `cp` - Copy Files or Directories
```bash
cp source.txt destination.txt         # Copy a file
cp -r /source/dir /destination/dir    # Copy a directory recursively
```

### `mv` - Move or Rename Files
```bash
mv oldname.txt newname.txt            # Rename file
mv /path/to/file /new/path/           # Move file to another directory
```

### `rm` - Remove Files or Directories
```bash
rm file.txt                           # Delete file
rm -r folder/                         # Delete directory recursively
```

### `tar` - Archive and Unarchive
```bash
tar -czvf archive.tar.gz folder/     # Create compressed archive
tar -xzvf archive.tar.gz             # Extract compressed archive
```

### `unzip` - Extract ZIP Files
```bash
unzip file.zip
unzip -d /path/to/extract/ file.zip  # Extract to specific directory
```

### `zip` - Create ZIP Archive
```bash
zip archive.zip file1 file2
zip -r archive.zip folder/           # Archive folder recursively
```
