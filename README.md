Tested on Debian 11 (Bullseye) with Kamailio 5.4.4

- Add your required configuration on your MS Teams tenant
https://learn.microsoft.com/en-us/microsoftteams/direct-routing-connect-the-sbc

- Install required Kamailio Repositories:

  apt update && apt install -y kamailio* mariadb-server
  
- Configure MariaDB and set root password: mysql_secure_installation
  
 - Edit /etc/kamailio/kamctlrc file and add the required SIP domain and database info.
 - Run 'kamdbctl create' to create kamailio database
 
 - Edit the /etc/kamailio/tls.cfg file and add your TLS certificates (cert, privkey and ca_list)
 
 - Replace both private and public IPs in the listen option with yours in /etc/kamailio/kamailio.cfg
 - Change your Kamailio public FQDN in both /etc/kamailio/dispatcher.list and /etc/kamailio/kamailio.cfg (default is teams.sipxtel.com)
 - Add your Public Kamailio FQDN and MS Teams domain in your local domain database (kamctl domain add <domain>) and reload after finished (kamctl domain reload)
 
  MS Teams FQDNs: sip.pstnhub.microsoft.com, sip2.pstnhub.microsoft.com, sip3.pstnhub.microsoft.com
  
  Important notes: can't use self-signed certs.... your Kamailio FQDN needs to be in the CN and SAN fields.
  
![image](https://user-images.githubusercontent.com/114504748/192582223-0e628e8d-d20e-4488-bbdf-9d673b10f476.png)

![image](https://user-images.githubusercontent.com/114504748/192582410-44acdcfb-27cb-4178-9ddb-23b0ce5742a2.png)

![image](https://user-images.githubusercontent.com/114504748/192593207-1bef0e01-d276-468d-94ae-db8b3bfcb009.png)


![image](https://user-images.githubusercontent.com/114504748/192584173-5e78f003-1d83-4169-9d11-f416ac20fcfb.png)


