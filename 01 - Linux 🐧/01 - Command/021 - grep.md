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

---

**Match whole word or line**

```bash
toor@gnu:~$ printf 'par value\nheir apparent\n' | grep -w 'par'
par value
```

---

**Line Anchors**

There are two line anchors:
• ˆ metacharacter restricts the matching to start of line
• $ metacharacter restricts the matching to end of line

```bash
toor@gnu:~$ # lines starting with 'pa'
toor@gnu:~$ printf 'spared no one\npar\nspar\ndare' | grep '^pa'
par
```
```bash
toor@gnu:~$ # lines ending with 'ar'
toor@gnu:~$ printf 'spared no one\npar\nspar\ndare' | grep 'ar$'
par
spar
```

```bash
toor@gnu:~$ # lines containing only 'par'
toor@gnu:~$ printf 'spared no one\npar\nspar\ndare' | grep '^par$'
par
```
```bash
toor@gnu:~$ printf 'spared no one\npar\nspar\ndare' | grep -x 'par'
par
```
---

**Word Anchors**

```bash
toor@gnu:~$ cat word_anchors.txt
sub par
spar
apparent effort
two spare computers
cart part tart mart
```

```bash
toor@gnu:~$ # match words starting with 'par'
toor@gnu:~$ grep '\bpar' word_anchors.txt
sub par
cart part tart mart
```

```bash
toor@gnu:~$ # match words ending with 'par'
toor@gnu:~$ grep 'par\b' word_anchors.txt
sub par
spar
```
---

**Alternation**

```bash
toor@gnu:~$ # match either 'cat' or 'dog'
toor@gnu:~$ printf 'I like cats\nI like parrots\nI like dogs' | grep 'cat\|dog'
I like cats
I like dogs
```

---

**Customizing separators**


```bash
toor@gnu:~$ grep -A0 --group-separator='*-----------*-----------*' 'toor@gnu.com' /var/log/mail.log
```
---


**Customize search path**


```bash
toor@gnu:~$ # without customizing
toor@gnu:~$ grep -Rl 'in'
.hidden
nested_group.txt
scripts/pi.py
context_matching/context.txt
```

```bash
toor@gnu:~$ # excluding 'scripts' directory and all hidden files
$ grep -Rl --exclude-dir='scripts' --exclude='.*' 'in'
nested_group.txt
context_matching/context.txt
```

```bash
toor@gnu:~$ # allow only filenames ending with '.txt' (will match hidden files too)
$ grep -Rl --include='*.txt' 'in'
nested_group.txt
context_matching/context.txt
```

```bash
toor@gnu:~$ # allow only filenames ending with '.txt' or '.py'
$ grep -Rl --include='*.txt' --include='*.py' 'in'
nested_group.txt
scripts/pi.py
context_matching/context.txt
```

```bash
toor@gnu:~$ # exclude all filenames ending with 'en' or '.txt'
$ printf '*en\n*.txt' | grep -Rl --exclude-from=- 'in'
scripts/pi.py
```

**Using find command**

```bash
toor@gnu:~$ # files (including hidden ones) less than 50 bytes
$ # '-type f' to match only files (not directories) and '-L' to follow links
$ find -L -type f -size -50c
./scripts/.key
./scripts/decode.sh
./scripts/pi.py
./patterns.txt
```

```bash
toor@gnu:~$ # apply 'grep' command to matched files
$ find -L -type f -size -50c -exec grep 'e$' {} +
./patterns.txt:hide
./patterns.txt:obscure
```