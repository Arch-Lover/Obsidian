`/searh some words` → search word → `n` → switch to next find word `--` `Shift + n ` switch to previous find word 

`d + / + word` → Delete from current cursor potion up to search result was deleted

`:s/old/new` --> Replace only one words in the line

`:s/old/new/g` --> Replace whole words in the line

`:1s/old/new/g` --> Replace whole words in line one

`:1,5/old/new/g` Replace whole words in line one to five

`:%s/old/new/g` Replace whole words

---

MAIL_PATH=/var/spool/mail

`:s#/var/spool/mail#/usr/local` --> Replace word with / pattern

`f + t` --> find t character (`;` will repeat the previuse command )
`Shift + f + T` --> find back word 

`t + b` --> one character before b
`Shift + t + b ` --> find back character before b