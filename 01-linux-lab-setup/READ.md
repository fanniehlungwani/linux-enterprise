# Linux Lab Setup

## Objective
Prepare enterprise Linux lab environment using 3 CentOS/RHEL virtual machines.

## Systems
- admin-server
- web-server
- client-server

## Tasks Completed
- Configured hostnames
- Verified connectivity
- Configured /etc/hosts
- Created administrative user
- Configured sudo access
- Installed Git

## Commands Used

### Set hostname
sudo hostnamectl set-hostname admin-server

### Create user
sudo useradd sysadmin

### Add sudo permissions
sudo usermod -aG wheel sysadmin
