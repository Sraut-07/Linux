**Local Port Forwarding**
Create local port that is connected to remote service

**Use Case**
1) Access internal servicess blocking Firewall
2) Access Services bound Localhost
3) Production enviroment Whare only SSH is Allowd


**Lab Setup**
This lab is performed using two local Virtual Machines running on the same host system

1) Clinet // Used Local Vm1
2) Server // Used Local Vme
3) SSh    // Port 22
4) Service // Port 80 and i used Nginx service

**Prerequisites**
. SSH access to remote server
. Web Service runnig on remote Server
.SSh service runnig

Step 1 :- Verify Web Service on Server
 Commands For Check

 Sudo systemctl status nginx.service
 OR
 Sudo systemctl satus apache2


 Check listening port

 sudo ss -tuln | grep :80

 Step 2 :- Check Direct Access Test From  Local VM Or Server

 curl http://10.10.10.3:80

 Fails Due to Localhost Binding


 Step 3 :- Create SSH Local Port Forwading 
 ssh -l 8081:localhost:80 vboxuser@10.10.10.3

 Command Breakdown
 8081 - Local port on client 10.10.10.2
 localhost:80 - Remote service on server
 vboxuser@10.10.10.3 - ssh login


 Step 4 :- Access Service locally in web
 http://localhost:8081

 Web service loads successfully


 Step 5 : Check Servr Logs 

 sudo tail -f /var/log/nginx/access.log

 Show 127.0.0.1 becuse traffic come through SSh tunnel 

 





















