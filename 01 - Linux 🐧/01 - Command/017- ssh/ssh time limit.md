Add this line to the `/etc/pam.d/sshd` file account section

```
account required pam_time.so
```

Add this line to the `/etc/security/time.conf` file time section

```
*;*;toor|foo;Al2100-2200

or

*;*;toor|foo;!Al2100-2200

or 

sshd;*;toor|foo;Al2100-2200
```

| *   | *   | User | time |
| --- | --- | ---- | ---- |
| witch service    |   terminel  |   foo   |   Mo Tu We Th Fr Sa Su Wk Wd Al   |