**How to Create Account on Zimbra using zmprov Tool**

```bash
toor@gnu:~$ su - zimbra


toor@gnu:~$ zmprov ca demo@zimbra.local "" displayName "Demo Account"
eb0eb381-4018-49d0-92d5-153291e6e18b


toor@gnu:~$ zmprov sp demo@zimbra.local password
```

---

**Get All Accounts**
```bash
toor@gnu:~$ zmprov -l gaa
```

---


**Add Account Alias**
```bash
toor@gnu:~$ zmprov aaa toor@gnu.dev xyz@gnu.dev

```
---

**Remove user account alias**
```bash
toor@gnu:~$ zmprov raa toor@gnu.dev xyz@gnu.dev
```

---

**Check all configuration parameters**

```bash 
toor@gnu:~$ zmprov -l gaa  -v gnu.dev
```
--- 

**check configuration parameter of particular user**

```bash
toor@gnu:~$ zmprov ga toor@gnu.dev
```

---

**List All admin Account**

```bash
toor@gnu:~$ zmprov gaaa
```

**Raname Account**

```bash
toor@gnu:~$ zmprov ra toor@gnu.dev toortoor@gnu.dev
```

---

**Delete Account**

```bash
toor@gnu:~$ zmprov da toor@gnu.dev

```
---

