# developing-on-windows10
win10上，为了便捷开发，一些配置和工具

## windows10
### 安装
https://www.microsoft.com/zh-cn/software-download/windows10
如果不能升级安装，可以下载iso文件硬盘安装
windows10专业版安装密钥：VK7JG-NPHTM-C97JM-9MPGT-3V66T
### cmd 激活
~~~
slmgr /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX
slmgr /skms kms.xspace.in
slmgr /ato
~~~
## 开启子系统
设置->针对开发人员->开发人员模式->启用或关闭windows功能->适用于linux的windows子系统
windows10商店->搜索->linux->ubuntu
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
Host github.com.developing-on-windows10
        HostName github.com
        User git
        IdentityFile /home/zongying/.ssh/id_rsa_github_developing-on-windows10
```
### 设置git
~~~
git clone https://github.com/lizongying/developing-on-windows10.git
git config user.name lizongying
git config user.email lizongying@msn.com
git remote rm origin
git remote add origin git@github.com.developing-on-windows10:lizongying/developing-on-windows10.git
git branch --set-upstream-to=origin/master master
~~~

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

## admin mongo
~~~
git clone https://github.com/mrvautin/adminMongo.git && cd adminMongo
npm install
npm start or node app
~~~
