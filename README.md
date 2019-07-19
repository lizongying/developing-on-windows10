# developing-on-windows10
win10上，为了便捷开发，一些配置和工具

## 生成github-key
~~~
ssh-keygen -t rsa -C "lizongying@msn.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/zongying/.ssh/id_rsa): /home/zongying/.ssh/id_rsa_github_developing-on-windows10
~~~
## 粘贴到github->Settings->Deploy keys->Add deploy key
Title->lizongying@msn.com
Key->
~~~
cat /home/zongying/.ssh/id_rsa_github_developing-on-windows10
~~~
Allow write access->yes
~~~
vim ~/.ssh/config
~~~
```
Host github.developing-on-windows10
        HostName github.com
        User git
        IdentityFile /home/zongying/.ssh/id_rsa_developing-on-windows10
```

