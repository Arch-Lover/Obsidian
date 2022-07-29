```bash
rsync ~/original/* ~/backup
```

```bash
rsync -r ~/original/* ~/backup ## for Directory use "-r" option
```

The end of etch path if use " / " the contents will be copied Otherwise only the FOLDER will be copied.

```bash
-a ## Keep Archive, Permission, Time modifation, Group, Owner
```

```bash
--dry-run -v 
```

```bash
-zPaAXv --dry-run
```