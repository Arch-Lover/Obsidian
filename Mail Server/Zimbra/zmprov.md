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


**print attribute name of all attributes**

```bash
toor@gnu:~$ zmprov desc

```

---

**print attribute name and all account attributes**

```bash
toor@gnu:~$ zmprov desc -v

```
---

```
toor@gnu.dev:~$ zmprov help account

  addAccountAlias(aaa) {name@domain|id} {alias@domain}

  createAccount(ca) {name@domain} {password} [attr1 value1 [attr2 value2...]]

  createDataSource(cds) {name@domain} {ds-type} {ds-name} zimbraDataSourceEnabled {TRUE|FALSE} zimbraDataSourceFolderId {folder-id} [attr1 value1 [attr2 value2...]]

  createIdentity(cid) {name@domain} {identity-name} [attr1 value1 [attr2 value2...]]

  createSignature(csig) {name@domain} {signature-name} [attr1 value1 [attr2 value2...]]

  deleteAccount(da) {name@domain|id}

  deleteDataSource(dds) {name@domain|id} {ds-name|ds-id}

  deleteIdentity(did) {name@domain|id} {identity-name}

  deleteSignature(dsig) {name@domain|id} {signature-name}

  getAccount(ga) [-e] {name@domain|id} [attr1 [attr2...]]

  getDataSources(gds) {name@domain|id} [arg1 [arg2...]]

  getIdentities(gid) {name@domain|id} [arg1 [arg...]]

  getSignatures(gsig) {name@domain|id} [arg1 [arg...]]

  getAccountMembership(gam) {name@domain|id}

  getAllAccounts(gaa) [-v] [-e] [-s server] [{domain}]
    -- NOTE: getAllAccounts can only be used with "zmprov -l/--ldap"

  getAllAdminAccounts(gaaa) [-v] [-e] [attr1 [attr2...]]

  modifyAccount(ma) {name@domain|id} [attr1 value1 [attr2 value2...]]

  modifyDataSource(mds) {name@domain|id} {ds-name|ds-id} [attr1 value1 [attr2 value2...]]

  modifyIdentity(mid) {name@domain|id} {identity-name} [attr1 value1 [attr2 value2...]]

  modifySignature(msig) {name@domain|id} {signature-name|signature-id} [attr1 value1 [attr2 value2...]]

  removeAccountAlias(raa) {name@domain|id} {alias@domain}

  renameAccount(ra) {name@domain|id} {newName@domain}

  setAccountCos(sac) {name@domain|id} {cos-name|cos-id}

  setPassword(sp) {name@domain|id} {password}

```
