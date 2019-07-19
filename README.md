# developing-on-windows10
win10上，为了便捷开发，一些配置和工具

### ubuntu 安装git zsh oh-my-zsh
~~~
sudo apt-get install git
sudo apt-get install zsh
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
~~~
## github 建立项目仓库
### 生成github-key
~~~
ssh-keygen -t rsa -C "lizongying@msn.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/zongying/.ssh/id_rsa): /home/zongying/.ssh/id_rsa_github_developing-on-windows10
~~~
### 粘贴到github->Settings->Deploy keys->Add deploy key
Title->lizongying@msn.com
Key->
~~~
cat /home/zongying/.ssh/id_rsa_github_developing-on-windows10.pub
~~~
Allow write access->yes
### 配置项目使用单独的key
~~~
vim ~/.ssh/config
~~~
```
Host github.developing-on-windows10
        HostName github.com
        User git
        IdentityFile /home/zongying/.ssh/id_rsa_developing-on-windows10
```
## 部署到服务器
### 配置服务器简单连接(注意更改服务器ip)
```
Host product
        HostName 127.0.0.1
        Port 22
        User root
        IdentityFile /home/zongying/.ssh/id_rsa_product
```
### 登上服务器建立代码存储文件夹
```
ssh product
```
```
mkdir /app
```
### 服务器简单同步代码
~~~
vim  ~/.bash_profile
~~~
~~~
alias rsync_developing-on-windows10='rsync -avz --progress --delete --exclude ".git" --exclude ".gitignore" --exclude ".idea" /mnt/c/IdeaProjects/developing-on-windows10 product:/app'
~~~
### 重新开启终端的时候自动加载bash_profile
~~~
vim ~/.zshrc
~~~
~~~
source ~/.bash_profile
~~~
## IntelliJ IDEA 免注册
### 修改host
~~~
vim /mnt/c/Windows/System32/drivers/etc/hosts
~~~
~~~
0.0.0.0 account.jetbrains.com
0.0.0.0 www.jetbrains.com
~~~
### http://idea.lanyus.com/->获取注册码
