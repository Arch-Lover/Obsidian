```bash
useradd -m -g users -G wheel -s /bin/bash vbox
```

```bash
useradd -m -d /home/reza -c "The Personal User" -s /bin/bash -G sudo,adm,mail reza
```

```bash
-m, --create-home
           Create the user's home directory if it does not exist. The files and directories
           contained in the skeleton directory (which can be defined with the -k option)
           will be copied to the home directory.
```

```bash
-b, --base-dir BASE_DIR
           The path prefix for a new user's home directory. The user's name will be affixed
           to the end of BASE_DIR to form the new user's home directory name, if the -d
           option is not used when creating a new account.
```

```bash
-c, --comment COMMENT
           Any text string. It is generally a short description of the login, and is
           currently used as the field for the user's full name.
```

```bash
-s, --shell SHELL
           The name of the user's login shell. The default is to leave this field blank,
           which causes the system to select the default login shell specified by the SHELL
           variable in /etc/default/useradd, or an empty string by default.
```

```bash
-G, --groups GROUP1[,GROUP2,...[,GROUPN]]]
           A list of supplementary groups which the user is also a member of. Each group is
           separated from the next by a comma, with no intervening whitespace. The groups
           are subject to the same restrictions as the group given with the -g option. The
           default is for the user to belong only to the initial group.
```

```bash
useradd -e 2022-02-12 u2
```

```bash
-e, --expiredate EXPIRE_DATE
           The date on which the user account will be disabled. The date is specified in the
           format YYYY-MM-DD.
```