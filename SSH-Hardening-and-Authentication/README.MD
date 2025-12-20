A practical repository focused on SSH hardening and authentication. Covers key-based access, root login protection, Fail2Ban, user/IP restrictions, and production-ready security best practices for Linux 
and cloud servers.
 
**Disable Root Login via SSH##
-Components
1)Client Machine

2️)SSH Client

OpenSSH

3️) Target Server

4)SSH service (sshd) running

##Perequisites

-SSH access to the server

-A non-root user with sudo privileges

-SSH service status check:

-systemctl status sshd
##Steps
-Step 1: Connect to the Server
ssh user@server_ip

-Step 2: Edit SSH Configuration
sudo nano /etc/ssh/sshd_config

-Step 3: Disable Root Login

Add or modify:

PermitRootLogin no

-Step 4: Restart SSH Service
sudo systemctl restart sshd

-Step 5: Verify
ssh root@server_ip


Expected result:

Permission denied

