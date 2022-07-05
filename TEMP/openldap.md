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


[root@server1 ~]# ldapmodify -Y EXTERNAL -H ldapi:/// -f config.ldif    
SASL/EXTERNAL authentication started  
SASL username: gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth  
SASL SSF: 0  
modifying entry "olcDatabase={2}hdb,cn=config"  
  
modifying entry "olcDatabase={2}hdb,cn=config"  
  
modifying entry "olcDatabase={2}hdb,cn=config"  
  
modifying entry "cn=config"  
  
modifying entry "olcDatabase={1}monitor,cn=config"
---




[root@server1 ~]# vim structure.ldif

dn: dc=example,dc=com
dc: example
objectClass: top
objectClass: domain

dn: ou=people,dc=example,dc=com
ou: people
objectClass: top
objectClass: organizationalUnit

dn: ou=group,dc=example,dc=com
ou: group
objectClass: top
objectClass: organizationalUnit


[root@server1 ~]# ldapadd -x -W -D "cn=Manager,dc=example,dc=com" -f structure.ldif    
Enter LDAP Password:    
ldap_bind: Invalid credentials (49)  
[root@server1 ~]# ldapadd -x -W -D "cn=Manager,dc=example,dc=com" -f structure.ldif    
Enter LDAP Password:    
adding new entry "dc=example,dc=com"  
  
adding new entry "ou=people,dc=example,dc=com"  
  
adding new entry "ou=group,dc=example,dc=com"




[root@server1 ~]# ldapsearch -x -W -D "cn=Manager,dc=example,dc=com" -b "dc=example,dc=com" -s sub "(objectclass=organizationalUnit)"  
Enter LDAP Password:    
# extended LDIF  
#  
# LDAPv3  
# base <dc=example,dc=com> with scope subtree  
# filter: (objectclass=organizationalUnit)  
# requesting: ALL  
#  
  
# people, example.com  
dn: ou=people,dc=example,dc=com  
ou: people  
objectClass: top  
objectClass: organizationalUnit  
  
# group, example.com  
dn: ou=group,dc=example,dc=com  
ou: group  
objectClass: top  
objectClass: organizationalUnit  
  
# search result  
search: 2  
result: 0 Success  
  
# numResponses: 3  
# numEntries: 2


---


vim group.ldif

dn: cn=ldapusers,ou=group,dc=example,dc=com
objectClass: posixGroup
cn: ldapusers
gidNumber: 4000


ldapadd -x -W -D "cn=Manager,dc=example,dc=com" -f group.ldif




---
cd /usr/share/migrationtools/

vim migrate_common.ph

$DEFAULT_MAIL_DOMAIN = "example.com";


$DEFAULT_BASE = "dc=example,dc=com";


cd
---

grep toor /etc/passwd

grep toor /etc/passwd > passwd


/usr/share/migrationtools/migrate_passwd.pl passwd user.ldif

---
vim user.ldif


dn: uid=toor,ou=People,dc=example,dc=com  
uid: toor  
cn: Reza Shokri  
objectClass: account  
objectClass: posixAccount  
objectClass: top  
objectClass: shadowAccount  
userPassword: {crypt}$6$DWDMQPVEpcQGe0es$JbWU1BVQ7xs9baznsNsku5tuH67TIffknD7a8/XUJDESxfmyg6Fmc/KNNDCOYFQneJH9Bln6n7Ntt6U4GWPaE.  
shadowMin: 0  
shadowMax: 99999  
shadowWarning: 7  
loginShell: /bin/bash  
uidNumber: 1000  
gidNumber: 1000  
homeDirectory: /home/toor  
gecos: Reza Shokri

	|
	|

dn: uid=fred,ou=People,dc=example,dc=com  
uid: fred  
cn: fred  
objectClass: account  
objectClass: posixAccount  
objectClass: top  
objectClass: shadowAccount  
userPassword: {crypt}$6$DWDMQPVEpcQGe0es$JbWU1BVQ7xs9baznsNsku5tuH67TIffknD7a8/XUJDESxfmyg6Fmc/KNNDCOYFQneJH9Bln6n7Ntt6U4GWPaE.  
shadowMin: 0  
shadowMax: 99999  
shadowWarning: 7  
loginShell: /bin/bash  
uidNumber: 4000  
gidNumber: 4000  
homeDirectory: /home/fred  
gecos: fred bloggs

---

[root@server1 ~]# ldapadd -x -W -D "cn=Manager,dc=example,dc=com" -f user.ldif    
Enter LDAP Password:    
adding new entry "uid=fred,ou=People,dc=example,dc=com"

```

```bash
[root@server2 ~]# echo "10.10.10.101 server1.example.com" >> /etc/hosts

[root@server2 ~]# ping server1.example.com  
PING server1.example.com (10.10.10.101) 56(84) bytes of data.  
64 bytes from server1.example.com (10.10.10.101): icmp_seq=1 ttl=64 time=0.733 ms  
64 bytes from server1.example.com (10.10.10.101): icmp_seq=2 ttl=64 time=0.393 ms  
64 bytes from server1.example.com (10.10.10.101): icmp_seq=3 ttl=64 time=0.369 ms  
64 bytes from server1.example.com (10.10.10.101): icmp_seq=4 ttl=64 time=0.400 ms


yum install oddjob oddjob-mkhomedir


systemctl start oddjobd


systemctl enable oddjobd


yum install openldap-clients nss-pam-ldapd


authconfig --enableldap --ldapserver=server1.example.com --ldapbasedn="dc=example,dc=com" --enablemkhomedir --update



[root@server2 ~]# grep passwd /etc/nsswitch.conf  
#passwd:    db files nisplus nis  
passwd:     files sss ldap


[root@server2 ~]# geten  
getenforce  getent         
[root@server2 ~]# getent passwd    
root:x:0:0:root:/root:/bin/bash  
bin:x:1:1:bin:/bin:/sbin/nologin  
daemon:x:2:2:daemon:/sbin:/sbin/nologin  
adm:x:3:4:adm:/var/adm:/sbin/nologin  
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin  
sync:x:5:0:sync:/sbin:/bin/sync  
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown  
halt:x:7:0:halt:/sbin:/sbin/halt  
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin  
operator:x:11:0:operator:/root:/sbin/nologin  
games:x:12:100:games:/usr/games:/sbin/nologin  
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin  
nobody:x:99:99:Nobody:/:/sbin/nologin  
systemd-network:x:192:192:systemd Network Management:/:/sbin/nologin  
dbus:x:81:81:System message bus:/:/sbin/nologin  
polkitd:x:999:998:User for polkitd:/:/sbin/nologin  
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin  
postfix:x:89:89::/var/spool/postfix:/sbin/nologin  
chrony:x:998:996::/var/lib/chrony:/sbin/nologin  
toor:x:1000:1000:Reza Shokri:/home/toor:/bin/bash  
nscd:x:28:28:NSCD Daemon:/:/sbin/nologin  
nslcd:x:65:55:LDAP Client User:/:/sbin/nologin  
fred:x:4000:4000:fred bloggs:/home/fred:/bin/bash


[root@server2 ~]# su - fred  
Creating home directory for fred.  
[fred@server2 ~]$





```