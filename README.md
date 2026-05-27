# Google Cloud Persistent Disk Management Project

## Overview
This project demonstrates how to create and manage Persistent Disks in Google Cloud Compute Engine using Cloud Shell and Linux commands.

The project includes:
- VM instance creation
- Persistent disk creation
- Disk attachment
- Linux filesystem formatting
- Disk mounting
- Auto-mount configuration using /etc/fstab

## Technologies Used
- Google Cloud Platform (GCP)
- Compute Engine
- Cloud Shell
- Linux (Debian)
- gcloud CLI

## Commands Used

### Set Region and Zone
```bash
gcloud config set compute/zone us-central1-b
gcloud config set compute/region us-central1
```

### Create VM Instance
```bash
gcloud compute instances create gcelab --zone us-central1-b --machine-type e2-standard-2
```

### Create Persistent Disk
```bash
gcloud compute disks create mydisk --size=200GB --zone us-central1-b
```

### Attach Disk
```bash
gcloud compute instances attach-disk gcelab --disk mydisk --zone us-central1-b
```

### SSH into VM
```bash
gcloud compute ssh gcelab --zone us-central1-b
```

### Create Mount Directory
```bash
sudo mkdir /mnt/mydisk
```

### Format Disk
```bash
sudo mkfs.ext4 -F -E lazy_itable_init=0,lazy_journal_init=0,discard /dev/disk/by-id/scsi-0Google_PersistentDisk_persistent-disk-1
```

### Mount Disk
```bash
sudo mount -o discard,defaults /dev/disk/by-id/scsi-0Google_PersistentDisk_persistent-disk-1 /mnt/mydisk
```

## Key Learnings
- Persistent Disk lifecycle
- Linux filesystem mounting
- Cloud storage management
- SSH access
- Auto-mount configuration

## Challenges Faced
- Nano editor paste issue on MacBook Air
- Understanding Linux mount process
- Understanding persistent disk migration workflow

## Outcome
Successfully created and managed a Persistent Disk in Google Cloud Compute Engine.
