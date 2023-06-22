```log
root@DESKTOP-N2LR1VA MINGW64 /d/javaworkspace/spring-batch/spring-batch (main)
git push -u origin main
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

**原因分析**
Permission denied (publickey) 没有权限的publickey ，出现这错误一般是以下两种原因
客户端与服务端未生成 ssh key
客户端与服务端的ssh key不匹配

客户端生成ssh key
```bash
ssh-keygen -t rsa -C "****@qq.com"
```

途中会让你输入密码啥的，不需要管，一路回车即可，会生成你的ssh key。（如果重新生成的话会覆盖之前的ssh key。）


ssh -v git@github.com

最后两句会出现
　　No more authentication methods to try.  
　　Permission denied (publickey).



 ssh-agent -s


ssh-add ~/.ssh/id_rsa


去C:\Users\root\.ssh下面找到id_rsa.pub文件，复制去 https://github.com/root/spring-batch-learning/settings/keys  
重新deploy key，粘贴进去就行
git push -u origin main
Warning: Permanently added the RSA host key for IP address '192.30.255.113' to the list of known hosts.
Enumerating objects: 30, done.
Counting objects: 100% (30/30), done.
Delta compression using up to 16 threads
Compressing objects: 100% (19/19), done.
Writing objects: 100% (30/30), 53.37 KiB | 323.00 KiB/s, done.
Total 30 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:root/spring-batch-learning.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.

成功


git clone失败
git clone https://github.com/guqing/blossom-fall.git
Cloning into 'blossom-fall'...
fatal: unable to access 'https://github.com/guqing/blossom-fall.git/': OpenSSL SSL_connect: Connection was reset in connection to github.com:443

root@DESKTOP-N2LR1VA MINGW64 /d/文档/码云项目下载/guqing-blossom-fall
git config --global http.sslBackend "openssl"

root@DESKTOP-N2LR1VA MINGW64 /d/文档/码云项目下载/guqing-blossom-fall
git config --global http.sslCAInfo "D:\soft\Git\Git\mingw64\ssl\cert.pem"

root@DESKTOP-N2LR1VA MINGW64 /d/文档/码云项目下载/guqing-blossom-fall
git clone https://github.com/guqing/blossom-fall.git
Cloning into 'blossom-fall'...
fatal: unable to access 'https://github.com/guqing/blossom-fall.git/': OpenSSL SSL_read: Connection was reset, errno 10054
这里还是不行，马的

root@DESKTOP-N2LR1VA MINGW64 /d/文档/码云项目下载/guqing-blossom-fall
git config --global http.sslVerify "false"

root@DESKTOP-N2LR1VA MINGW64 /d/文档/码云项目下载/guqing-blossom-fall
git clone https://github.com/guqing/blossom-fall.git
Cloning into 'blossom-fall'...
fatal: unable to access 'https://github.com/guqing/blossom-fall.git/': OpenSSL SSL_read: Connection was reset, errno 10054
还是不行，放弃了，fork仓库过来

root@DESKTOP-N2LR1VA MINGW64 /d/文档/码云项目下载/guqing-blossom-fall
git clone https://github.com/root/blossom-fall.git
Cloning into 'blossom-fall'...
remote: Enumerating objects: 1068, done.
remote: Counting objects: 100% (154/154), done.
remote: Compressing objects: 100% (78/78), done.
remote: Total 1068 (delta 98), reused 127 (delta 76), pack-reused 914
Receiving objects: 100% (1068/1068), 39.43 MiB | 100.00 KiB/s, done.
Resolving deltas: 100% (269/269), done.



2022.9.23,pull自己仓库时出错了，忘记passphrase了，只能重新生成ssh了
root@192 .ssh % ls
id_rsa		id_rsa.pub	known_hosts	known_hosts.old
root@192 .ssh % ssh-add id_rsa
Enter passphrase for id_rsa:
root@192 .ssh % ssh-keygen -t rsa -b 4096 -C "*****@qq.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/root/.ssh/id_rsa): ??????
Enter passphrase (empty for no passphrase): ??????
Enter same passphrase again: ??????
Your identification has been saved in ??????
Your public key has been saved in ??????.pub
The key fingerprint is:
。。。
root@192 .ssh % ls -l
total 48
-rw-------  1 root  staff  3434  9 23 11:23 ??????
-rw-r--r--  1 root  staff   743  9 23 11:23 ??????.pub
-rw-------@ 1 root  staff  2655  6 18 15:24 id_rsa
-rw-r--r--@ 1 root  staff   577  9 23 11:15 id_rsa.pub
-rw-------@ 1 root  staff  1499  6 19 09:14 known_hosts
-rw-------  1 root  staff   753  6 19 09:14 known_hosts.old
被自己蠢死，文件名变成??????了，把??????.pub内容复制到github账户的ssh中



重新生成一次
root@192 ~ % ssh-keygen -t rsa -C "******@qq.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/root/.ssh/id_rsa):
/Users/root/.ssh/id_rsa already exists.
Overwrite (y/n)? y
Enter passphrase (empty for no passphrase): ???
Enter same passphrase again: ???
Your identification has been saved in /Users/root/.ssh/id_rsa
Your public key has been saved in /Users/root/.ssh/id_rsa.pub
The key fingerprint is:
...
root@192 ~ % ls
Desktop				Virtual Machines.localized
Documents			chromeDwon
Downloads			code
Library				developertools
Movies				git_repository
Music				logs
Pictures			nacos
Public				zlibarybooks
Safaridown
root@192 ~ % cd .ssh
root@192 .ssh % ls
??????		id_rsa		known_hosts
??????.pub	id_rsa.pub	known_hosts.old
root@192 .ssh % ls -l
total 48
-rw-------  1 root  staff  3434  9 23 11:23 ??????
-rw-r--r--@ 1 root  staff   743  9 23 11:23 ??????.pub
-rw-------@ 1 root  staff  2655  9 23 11:53 id_rsa
-rw-r--r--@ 1 root  staff   571  9 23 11:53 id_rsa.pub
-rw-------@ 1 root  staff  1499  6 19 09:14 known_hosts
-rw-------  1 root  staff   753  6 19 09:14 known_hosts.old
root@192 .ssh % cat id_rsa.pub
Enter passphrase for key '/Users/root/.ssh/id_rsa':
Hi root! You've successfully authenticated, but GitHub does not provide shell access.
root@192 .ssh %


查找github最快的ip，
https://tool.chinaz.com/speedtest/github.com
找到最快的ip，修改hosts后修改立即生效
sudo vim /etc/hosts
写入 IP github.com
wq保存退出
输入 sudo killall -HUP mDNSResponder 使其立即生效


```log
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the RSA key sent by the remote host is
SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.
Please contact your system administrator.
Add correct host key in /root/.ssh/known_hosts to get rid of this message.
Offending RSA key in /root/.ssh/known_hosts:1
Host key for github.com has changed and you have requested strict checking.
Host key verification failed.
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```
**解决办法**
```bash
ssh-keygen -R github.com
```



