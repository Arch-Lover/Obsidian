**Zimbra backup and recovery password**

```bash
zimbra@gnu:~$ zmprov -l ga toor userPassword
# name toor@gnu.dev
userPassword: {SSHA}IamjLcOTWbk13/Y1Ud+oi/8NDIcQoctM

zimbra@gnu:~$ zmprov sp toor@gnu.dev PASSWORD

zimbra@gnu:~$ zmprov ma atoor@gnu.dev userPassword "{SSHA}IamjLcOMWbk13/Y1Yd+oi/8NDIcQoctM"
```