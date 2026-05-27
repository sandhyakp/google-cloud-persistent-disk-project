````markdown
# Google Cloud Persistent Disk Management Project

## Overview

This project demonstrates how to create and manage Persistent Disks in Google Cloud Compute Engine using Cloud Shell and Linux commands.

The project was completed as part of hands-on Google Cloud Skills / Arcade learning and includes VM creation, disk attachment, filesystem formatting, Linux mounting, and auto-mount configuration.

---

## Project Objective

The objective of this project was to understand:

- Google Cloud Compute Engine
- Persistent Disk lifecycle
- Linux filesystem mounting
- Cloud Shell and gcloud CLI
- Storage management in cloud environments

---

## Technologies Used

- Google Cloud Platform (GCP)
- Compute Engine
- Cloud Shell
- Linux (Debian)
- gcloud CLI

---

## Tasks Performed

### 1. Configured Region and Zone

```bash
gcloud config set compute/zone us-central1-b
gcloud config set compute/region us-central1
```

---

### 2. Created VM Instance

```bash
gcloud compute instances create gcelab --zone us-central1-b --machine-type e2-standard-2
```

Created a Compute Engine VM instance named:

- gcelab

---

### 3. Created Persistent Disk

```bash
gcloud compute disks create mydisk --size=200GB --zone us-central1-b
```

Created:
- 200 GB Persistent Disk

Disk name:
- mydisk

---

### 4. Attached Persistent Disk to VM

```bash
gcloud compute instances attach-disk gcelab --disk mydisk --zone us-central1-b
```

Attached the newly created persistent disk to the virtual machine instance.

---

### 5. Connected to VM using SSH

```bash
gcloud compute ssh gcelab --zone us-central1-b
```

Used SSH access through Cloud Shell to manage the Linux VM.

---

### 6. Verified Attached Disk

```bash
ls -l /dev/disk/by-id/
```

Verified the attached disk:

```text
scsi-0Google_PersistentDisk_persistent-disk-1
```

---

### 7. Created Mount Directory

```bash
sudo mkdir /mnt/mydisk
```

Created mount point for the persistent disk.

---

### 8. Formatted Persistent Disk

```bash
sudo mkfs.ext4 -F -E lazy_itable_init=0,lazy_journal_init=0,discard /dev/disk/by-id/scsi-0Google_PersistentDisk_persistent-disk-1
```

Formatted the disk using ext4 filesystem.

---

### 9. Mounted Persistent Disk

```bash
sudo mount -o discard,defaults /dev/disk/by-id/scsi-0Google_PersistentDisk_persistent-disk-1 /mnt/mydisk
```

Mounted the disk successfully inside Linux.

---

### 10. Configured Auto-Mount

Edited:

```text
/etc/fstab
```

Added:

```text
/dev/disk/by-id/scsi-0Google_PersistentDisk_persistent-disk-1 /mnt/mydisk ext4 defaults 1 1
```

This ensures the disk automatically mounts after VM restart.

---

## Challenges Faced

### Nano Editor Paste Issue on MacBook Air

While editing `/etc/fstab` inside nano editor, the standard `CTRL + V` shortcut did not work on macOS.

Solution:
- Used `Command (⌘) + V` for paste inside nano editor.

---

### Understanding Linux Mounting Process

Initially there was confusion between:

- Attaching disk in GCP
- Mounting disk in Linux

Key understanding:

- GCP Attach = hardware connection
- Linux Mount = filesystem accessibility

---

### Understanding Persistent Disk Migration Workflow

Learned the correct sequence for persistent disk migration:

```text
Unmount → Snapshot → Create Disk → Create Instance → Attach Disk
```

---

## Key Learnings

- Persistent Disk management in GCP
- Linux filesystem formatting
- Disk mounting and auto-mounting
- SSH access using Cloud Shell
- Compute Engine basics
- Storage lifecycle management

---

## Screenshots Included

- VM Instance
- Persistent Disk
- Attached Disk
- Cloud Shell Terminal Output

---

## Project Demo Video

YouTube Video:
https://youtu.be/Xtr1nzIbZjI

---

## Outcome

Successfully created, attached, formatted, and mounted a Persistent Disk in Google Cloud Compute Engine using Linux commands and Cloud Shell.

This project provided practical hands-on experience with cloud infrastructure and storage management in Google Cloud Platform.

```
````
