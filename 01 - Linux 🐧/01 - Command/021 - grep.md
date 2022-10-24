**Case insensitive search**

```bash
toor@gnu:~$ cat Case-insensitive-search

error
Error
ERROR
```

```bash
toor@gnu:~$ grep -i 'error' Case-insensitive-search

error
Error
ERROR
```

---

**Invert matching lines**

```bash
toor@gnu:~$ seq 5 | grep -v '3'
1
2
4
5
```

---

**Line number and count**

```bash
toor@gnu:~$ printf 'line1\nline2\nline3' | grep -n 'line'
1:line1
2:line2
3:line3
````

```bash
toor@gnu:~$ printf 'goal\nrate\neat\npit' | grep -c 'g'
1
```

---

**Limiting output lines**

```bash
seq 1000 | grep -m4 '2'
2
12
20
21
```

---

**Multiple search strings**

```bash
toor@gnu:~$ cat name.list
eager
eagle
eagre
eared
earls
early
earns
earea
```

```bash
toor@gnu:~$ grep -e eager -e earns name.list
eager
earns
```

```bash
toor@gnu:~$ grep -f search_strings.txt programming_quotes.txt
```

```bash
toor@gnu:~$ grep -f search_strings.txt -e 'twice' programming_quotes.txt
```
---

**Filename instead of matching lines**

• -l will list files matching the pattern
• -L will list files NOT matching the pattern


```bash
toor@gnu:~$ grep -l 'are' programming_quotes.txt search_strings.txt
```