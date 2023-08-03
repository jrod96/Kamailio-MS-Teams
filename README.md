**Tested on Debian 11 (Bullseye) with Kamailio 5.4.4**

- Add your required configuration on your MS Teams tenant
https://learn.microsoft.com/en-us/microsoftteams/direct-routing-connect-the-sbc

- Install required Kamailio Repositories:

  apt update \\<br>
  && apt install -y kamailio* \\<br>
  && apt install -y mariadb-server
  
- Configure MariaDB and set root password with the mysql script:<br>
  
  mysql_secure_installation
  
 - Edit /etc/kamailio/kamctlrc file and add the required SIP domain and database info.
 - Run 'kamdbctl create' to create kamailio database
 
 - Edit the /etc/kamailio/tls.cfg file and add your TLS certificates (cert, privkey and ca_list)
 
 - Replace both private and public IPs in the listen option with yours in /etc/kamailio/kamailio.cfg
 - Change your Kamailio public FQDN in both /etc/kamailio/dispatcher.list and /etc/kamailio/kamailio.cfg (default is teams.sipxtel.com)
 - Add your Public Kamailio FQDN and MS Teams domain in your local domain database (kamctl domain add <domain>) and reload after finished (kamctl domain reload)
 
  **MS Teams FQDNs:** <br>
  sip.pstnhub.microsoft.com<br>
  sip2.pstnhub.microsoft.com<br>
  sip3.pstnhub.microsoft.com
  
  **Important notes:** can't use self-signed certs.... your Kamailio FQDN needs to be in the CN and SAN fields.... I used let's encrypt in this example.
  If you are using the default CA list from linux, there could be cases in which the TLS handshake could not be established with Teams because missing   
  root/intermediate certificates in your trusted store. It can be fixed either installing the root/intermediate CAs being used by teams or creating your 
  own chain. 
  
  https://learn.microsoft.com/en-us/purview/encryption-office-365-tls-certificates-changes?view=o365-worldwide
  
  **Root/Intermediate CAs used by Teams:**
  
  Baltimore CyberTrust Root
  Microsoft RSA TLS CA 02
  DigiCert Global Root G2
  
  - Resources:<br>
  https://blog.opensips.org/2019/09/16/opensips-as-ms-teams-sbc/ <br>
  https://skalatan.de/en/blog/kamailio-sbc-teams
  
If there are no issues, you will be able to see the SIP OPTIONS coming in and going out.
  
![image](https://user-images.githubusercontent.com/114504748/192582223-0e628e8d-d20e-4488-bbdf-9d673b10f476.png)

![image](https://user-images.githubusercontent.com/114504748/192582410-44acdcfb-27cb-4178-9ddb-23b0ce5742a2.png)

![image](https://user-images.githubusercontent.com/114504748/192593207-1bef0e01-d276-468d-94ae-db8b3bfcb009.png)

 ![image](https://user-images.githubusercontent.com/114504748/192613467-fcacd1f3-501c-4846-917e-10733e2db1b3.png)

![image](https://user-images.githubusercontent.com/114504748/192584173-5e78f003-1d83-4169-9d11-f416ac20fcfb.png)


