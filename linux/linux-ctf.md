# ls 指令測試

### ls
```
lab@29d4cf5af0ab:~$ ls
base64.txt  flag  hex.txt
```
```
cat flag
```
### ls -l
```
lab@29d4cf5af0ab:~$ ls -l
total 12
-rw-rw-r-- 1 root root 46 Nov 20  2017 base64.txt
-rw-rw-r-- 1 root root 35 Nov 15  2017 flag
-rw-rw-r-- 1 root root 68 Nov 20  2017 hex.txt
```
### ls -Al
```

lab@29d4cf5af0ab:~$ ls -Al
total 28
-rw-r--r-- 1 lab  lab   220 Apr 26 14:48 .bash_logout
-rw-r--r-- 1 root root 3771 Apr 26 14:48 .bashrc
-rw-rw-r-- 1 root root   34 Nov 19  2017 .hidden
-rw-r--r-- 1 lab  lab   655 Apr 26 14:48 .profile
-rw-rw-r-- 1 root root   46 Nov 20  2017 base64.txt
-rw-rw-r-- 1 root root   35 Nov 15  2017 flag
-rw-rw-r-- 1 root root   68 Nov 20  2017 hex.txt


```
### ls -al
```
lab@29d4cf5af0ab:~$ ls -al
total 36
drwxr-xr-x 1 root root 4096 Apr 26 14:48 .
drwxr-xr-x 1 root root 4096 Apr 26 14:48 ..
-rw-r--r-- 1 lab  lab   220 Apr 26 14:48 .bash_logout
-rw-r--r-- 1 root root 3771 Apr 26 14:48 .bashrc
-rw-rw-r-- 1 root root   34 Nov 19  2017 .hidden
-rw-r--r-- 1 lab  lab   655 Apr 26 14:48 .profile
-rw-rw-r-- 1 root root   46 Nov 20  2017 base64.txt
-rw-rw-r-- 1 root root   35 Nov 15  2017 flag
-rw-rw-r-- 1 root root   68 Nov 20  2017 hex.txt
```
# 指令與指令參數
```
command(指令) line 
options 參數
```
## 指令參數的學習
```
ls -h
ls --h
ls -help
ls --help
```
```
到google 搜尋linux ls
```
```
