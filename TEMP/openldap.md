```bash
sudo hostnamectl set-hostname server1.example.com


[toor@server1 ~]$ hostname  
server1.example.com

sudo su -


echo "10.10.10.101 server1.example.com" >> /etc/hosts

ping erver1.example.com


yum install net-tools


[root@server1 ~]# netstat -ltn            
Active Internet connections (only servers)  
Proto Recv-Q Send-Q Local Address           Foreign Address         State         
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN        
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN        
tcp6       0      0 :::22                   :::*                    LISTEN        
tcp6       0      0 ::1:25                  :::*                    LISTEN


[root@server1 ~]# firewall-cmd --permanent --add-service=ldap    
success

[root@server1 ~]# firewall-cmd --reload  
success

yum install  -y openldap openldap-clients openldap-servers migrationtools

---


cp /usr/share/openldap-servers/DB_CONFIG.example /var/lib/ldap/DB_CONFIG

[root@server1 ~]# ls -l /var/lib/ldap/  
total 4  
-rw-r--r--. 1 root root 845 Jul  4 04:28 DB_CONFIG


slaptest


[root@server1 ~]# ls -l /var/lib/ldap/  
total 19020  
-rw-r--r--. 1 root root     2048 Jul  4 04:37 alock  
-rw-------. 1 root root  2367488 Jul  4 04:37 __db.001  
-rw-------. 1 root root 17457152 Jul  4 04:37 __db.002  
-rw-------. 1 root root  1884160 Jul  4 04:37 __db.003  
-rw-r--r--. 1 root root      845 Jul  4 04:28 DB_CONFIG



chown ldap.ldap /var/lib/ldap/*

systemctl start slapd

systemctl enable slapd

[root@server1 ~]# systemctl status  slapd  
● slapd.service - OpenLDAP Server Daemon  
  Loaded: loaded (/usr/lib/systemd/system/slapd.service; enabled; vendor preset: disabled)  
  Active: active (running) since Mon 2022-07-04 04:53:55 EDT; 43s ago  
    Docs: man:slapd  
          man:slapd-config  
          man:slapd-hdb  
          man:slapd-mdb  
          file:///usr/share/doc/openldap-servers/guide.html  
Main PID: 1608 (slapd)  
  CGroup: /system.slice/slapd.service  
          └─1608 /usr/sbin/slapd -u ldap -h ldapi:/// ldap:///  
  
Jul 04 04:53:49 server1.example.com runuser[1599]: pam_unix(runuser:session): session opened for user ldap by (uid=0)  
Jul 04 04:53:49 server1.example.com runuser[1599]: pam_unix(runuser:session): session closed for user ldap  
Jul 04 04:53:49 server1.example.com runuser[1601]: pam_unix(runuser:session): session opened for user ldap by (uid=0)  
Jul 04 04:53:49 server1.example.com runuser[1601]: pam_unix(runuser:session): session closed for user ldap  
Jul 04 04:53:49 server1.example.com runuser[1603]: pam_unix(runuser:session): session opened for user ldap by (uid=0)  
Jul 04 04:53:49 server1.example.com runuser[1603]: pam_unix(runuser:session): session closed for user ldap  
Jul 04 04:53:50 server1.example.com slapd[1606]: @(#) $OpenLDAP: slapd 2.4.44 (Feb 23 2022 17:11:27) $  
                                                        mockbuild@x86-01.bsys.centos.org:/builddir/build/BUILD/openldap-2.4.44/openldap-2.4...rs/slapd  
Jul 04 04:53:55 server1.example.com slapd[1606]: tlsmc_get_pin: INFO: Please note the extracted key file will not be protected with a PIN an...issions.  
Jul 04 04:53:55 server1.example.com slapd[1608]: slapd starting  
Jul 04 04:53:55 server1.example.com systemd[1]: Started OpenLDAP Server Daemon.  
Hint: Some lines were ellipsized, use -l to show in full.


[root@server1 ~]# netstat -ltn  
Active Internet connections (only servers)  
Proto Recv-Q Send-Q Local Address           Foreign Address         State         
tcp        0      0 0.0.0.0:389             0.0.0.0:*               LISTEN        
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN        
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN        
tcp6       0      0 :::389                  :::*                    LISTEN        
tcp6       0      0 :::22                   :::*                    LISTEN        
tcp6       0      0 ::1:25                  :::*                    LISTEN


[root@server1 ~]# netstat -lt  
Active Internet connections (only servers)  
Proto Recv-Q Send-Q Local Address           Foreign Address         State         
tcp        0      0 0.0.0.0:ldap            0.0.0.0:*               LISTEN        
tcp        0      0 0.0.0.0:ssh             0.0.0.0:*               LISTEN        
tcp        0      0 localhost:smtp          0.0.0.0:*               LISTEN        
tcp6       0      0 [::]:ldap               [::]:*                  LISTEN        
tcp6       0      0 [::]:ssh                [::]:*                  LISTEN        
tcp6       0      0 localhost:smtp          [::]:*                  LISTEN

cd /etc/openldap/schema/

ldapadd -Y EXTERNAL -H ldapi:/// -D "cn=config" -f cosine.ldif

ldapadd -Y EXTERNAL -H ldapi:/// -D "cn=config" -f nis.ldif

cd

slappasswd -s Password1 -n > rootpwd

[root@server1 ~]# cat rootpwd    
{SSHA}k640htpxw0jRIe2qrqhgTnfhrF2wszT2[root@server1 ~]#


---
vim config.ldif

dn: olcDatabase={2}hdb,cn=config
changetype: modify
replace: olcSuffix
olcSuffix: dc=example,dc=com

dn: olcDatabase={2}hdb,cn=config
changetype: modify
replace: olcRootDN
olcRootDN: cn=Manager,dc=example,dc=com

dn: olcDatabase={2}hdb,cn=config
changetype: modify
replace: olcRootPW
#Password is Password1 or add your own
olcRootPW: {SSHA}zPhLTnlzuDlz+L+pZBrb7fCGD7kZd6QG

dn: cn=config
changetype: modify
replace: olcLogLevel
olcLogLevel: 0

dn: olcDatabase={1}monitor,cn=config
changetype: modify
replace: olcAccess
olcAccess: {0}to * by dn.base="gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth" read by dn.base="cn=Manager,dc=example,dc=com" read by * none



---








```