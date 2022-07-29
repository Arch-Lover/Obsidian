```bash
➜  ~ hostname

server1.home.local
```

```bash
➜  # echo "192.168.99.20 server1.home.local" >> /etc/hosts
```

```bash
➜  ~ ping server1.home.local
``` 

```bash
➜  ~ netstat -ltn 

tcp  0  0.0.0.0:22  0.0.0.0:*  LISTEN
tcp  0  127.0.0.1:25  0.0.0.0:*  LISTEN

```

```bash
➜  # firewall-cmd --permenent --add-service =ldap 
```

```bash
➜  # firewall-cmd --reload 
```

```bash
➜  # sudo yum install -y openldap openldap-clients openldap-server migrationtools.noarch
```

```bash
➜  # cp /usr/share/openldap-servers/DB_CONFIG.example /var/lib/ldap/DB_CONFIG 
```

```bash
➜  # slaptest
```

```bash
➜  # chown ldap.ldap /var/lib/ldap/*
```

```bash
➜  # systemctl enable --now slapd
```

```bash
➜  ~ netstat -ltn 

tcp  0  0.0.0.0:22  0.0.0.0:*  LISTEN
tcp  0  127.0.0.1:25  0.0.0.0:*  LISTEN
tcp  0  0.0.0.0:389  0.0.0.0:*  LISTEN

```

```bash
➜  ~ netstat -lt 

tcp  0  0.0.0.0:ssh  0.0.0.0:*  LISTEN
tcp  0  127.0.0.1:smtp  0.0.0.0:*  LISTEN
tcp  0  0.0.0.0:ldap  0.0.0.0:*  LISTEN

```

```bash
➜  ~ cd /etc/openldap/schema

➜  # ldapadd -Y EXTERNAL -H ldapi:/// -D "cn=config" -f  consine.ldif 

➜  # ldapadd -Y EXTERNAL -H ldapi:/// -D "cn=config" -f  nis.ldif 
```

```bash
➜  # cd 

➜  # slappassword =s toorpass -n > rootpwd

➜  # rootpwd 
{SSHA}lksdldkgjdlskgjldkfjgldkfjglkdfjgldkfjglF
```

```bash
➜  # vi config.ldif 

olcSuffix: dc=example,dc=com
.
.
.
oldRootDN: cn=Manager,dc=example,dc=com
.
.
.
olcRootPW: {SSHA}lksdldkgjdlskgjldkfjgldkfjglkdfjgldkfjglF

	vim trick --> :r rootpwd
.
.
.
olcLogLevel: 0
.
.
.
olcAccess ....

vim --> :x
```

```bash
➜  # ldapmodify -Y EXTERNAL -H ldapi:/// -f config.ldif

```

```bash
➜  # cat structure.ldif 
```

```bash
➜  # ldapadd -x -W -D "cn=Manager,dc=example,dc=com" -f structure.ldif
```


```bash
➜  # ldapadd -x -W -D "cn=Manager,dc=example,dc=com" -b "dc=example,dc=com" -s sub "(objectclass=organizationalUnit)"
```


