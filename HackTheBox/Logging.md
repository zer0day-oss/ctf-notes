* Credentials given: wallace.everette / Welcome2026@
* Ports open: ```
53/tcp    open     domain           syn-ack
80/tcp    open     http             syn-ack
88/tcp    open     kerberos-sec     syn-ack
135/tcp   open     msrpc            syn-ack
139/tcp   open     netbios-ssn      syn-ack
389/tcp   open     ldap             syn-ack
445/tcp   open     microsoft-ds     syn-ack
464/tcp   open     kpasswd5         syn-ack
593/tcp   open     http-rpc-epmap   syn-ack
636/tcp   open     ldapssl          syn-ack
1412/tcp  filtered innosys          no-response
3268/tcp  open     globalcatLDAP    syn-ack
3269/tcp  open     globalcatLDAPssl syn-ack
5985/tcp  open     wsman            syn-ack
7599/tcp  filtered unknown          no-response
8530/tcp  open     unknown          syn-ack
8531/tcp  open     unknown          syn-ack
9389/tcp  open     adws             syn-ack
10696/tcp filtered unknown          no-response
25805/tcp filtered unknown          no-response
28762/tcp filtered unknown          no-response
28944/tcp filtered unknown          no-response
30222/tcp filtered unknown          no-response
30238/tcp filtered unknown          no-response
30869/tcp filtered unknown          no-response
41771/tcp filtered unknown          no-response
44859/tcp filtered unknown          no-response
47001/tcp open     winrm            syn-ack
49664/tcp open     unknown          syn-ack
49665/tcp open     unknown          syn-ack
49666/tcp open     unknown          syn-ack
49667/tcp open     unknown          syn-ack
49671/tcp open     unknown          syn-ack
49686/tcp open     unknown          syn-ack
49687/tcp open     unknown          syn-ack
49688/tcp open     unknown          syn-ack
49689/tcp open     unknown          syn-ack
49694/tcp open     unknown          syn-ack
49720/tcp open     unknown          syn-ack
49746/tcp open     unknown          syn-ack
49776/tcp open     unknown          syn-ack
53688/tcp filtered unknown          no-response
56829/tcp filtered unknown          no-response
62413/tcp filtered unknown          no-response

+ when I come back, make sure to set the dns for /etc/hosts to logging.htb.
+ I left off in the middle of winrm session with user msa_health$ with nt hash which was obtained with krbtgt ticket. Krbtgt ticket was obtained by grabbing the krb5.conf with nxc using the svc_recovery account due to having GenericWrite over msa_health$, leading to abuse of privilege to add shadowCredentials to userGroup. 
	+ credentials used: svc_recovery:Em3rg3ncyPa$$2026


