# What is path?
When you run a command in your terminal, the shell looks for that command in the director is defined.

```bash
[toor@pve1box1 bash]$ echo "$PATH"  
/usr/local/sbin:/usr/local/bin:/usr/bin:/usr/bin/site_perl:/usr/bin/vendor_perl:/usr/bin  
/core_perl
```
```bash
cat ~/profile
```
```bash
         
        # ~/.profile: executed by Bourne-compatible login shells.
         
        if [ "$BASH" ]; then
          if [ -f ~/.bashrc ]; then
            . ~/.bashrc
          fi
        fi
         
        mesg n || true
         
```
```bash
root@slax:~# ls -lda .pro* 
-rw-r--r-- 1 root root 148 Aug 17  2015 .profile

```
```bash
chmod 622 ~/profile
chown $USER:$USER ~/profile
```
Add this line to end of file (before mesg n || true command)
```bash
export PATH="PATH:$HOME/scrips"
```
```bash
source ~/profile
```