 **Remote Port Forwarding**

Remote Port Forwarding allows you to expose a service running on a local machine to a remote server through an encrypted SSH tunnel.


**Use Cases**
1) Provide access to a local/internal service

2)Production environments where only SSH (port 22) is allowed

Lab Setup

This lab is performed using two local Virtual Machines running on the same host system.
 
 **Component**
 1) Client VM -VM where the web service is running
 2) Server VM - VM that exposes the forwarded port
 3) SSH Port - 22
 4) Service - Nginx running on port 80

 **IP Details**

Client (Web Service) IP: 10.10.10.3

Server (SSH Server) IP: 10.10.10.2

**Prerequisites**

1) SSH access to the server VM

2) Web service (Nginx) running on the client VM

3) SSH service (sshd) running on the server VM

Step 1: Verify Web Service on Client VM (10.10.10.3)

sudo systemctl status nginx
# OR
sudo systemctl status apache2

Confirms that the web service is running

Step 2: Verify SSH Service on Server VM (10.10.10.2)

sudo systemctl status ssh
Check SSH port listening:
sudo ss -tuln | grep :22

Step 3: Verify Web Service Port on Client VM
sudo ss -tuln | grep :80

Step 4: Direct Access Test (Expected to Fail)

From Server VM (10.10.10.2):

curl http://10.10.10.3:80

Fails due to localhost binding or firewall restrictions

Step 5: Create SSH Remote Port Forwarding

Run this command on the Client VM (10.10.10.3):

ssh -fN -R 5555:localhost:80 username@10.10.10.2

Command Breakdown

-R → Remote port forwarding

-f → Run SSH in background

-N → Do not open remote shell

5555 → Port opened on server VM (10.10.10.2)

localhost:80 → Web service running on client VM

username@10.10.10.2 → SSH login to server VM

Step 6: Access the Service via Server VM on (10.10.10.2)

Open in browser or use curl:

curl http://localhost:5555

Web service loads successfully.

Step 7: Check Web Server Logs on Client VM
sudo tail -f /var/log/nginx/access.log

Why 127.0.0.1?

Traffic reaches Nginx through the SSH tunnel, which forwards requests locally on the client VM.

**Key Observations**

Port 80 is not exposed publicly

Only SSH port 22 is required

Access is encrypted and temporary

Tunnel closes when SSH session end