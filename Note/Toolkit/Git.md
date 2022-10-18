## Git 下载

- [淘宝镜像](http://npm.taobao.org/mirrors/git-for-windows/)
- [Git 官网](https://git-scm.com/)

## 本地配置和生成密钥对

### 一、配置用户全局名称和邮箱

```bash
git config --global user.name "fanfan"
git config --global user.email "zhangfanfan@email.cn"
```

### 二、生成密钥

```bash
# 一路回车即可(可以什么都不填)
ssh-keygen -t rsa -C "your_email@youremail.com"
```

### 三、添加密钥

**将上一步骤生成的密钥即.ssh/id_rsa.pub中内容全部复制。在github的 Settings-->SSH and GPG keys-->New SSH key，key中粘贴复制的内容(Title自定义)**

### 四、验证

```bash
ssh -T git@github.com
ssh -T git@gitee.com
```

## 创建本地仓库并连接远程仓库

### 一、新建一个文件夹，在该文件夹下初始化

```bash
git init
```

### 二、连接远程仓库

```bash
git remote add origin + 项目的SSH OR Https
```

### 三、从远程仓库pull文件

```bash
git pull origin master
```

### 四、将本地文件push到远程仓库

```bash
git status　　　　　　　　　　# 查看工作目录的状态
git add <file>　　　　　　　 # 将文件添加到暂存区
git commit -m "commnet" 　　# 提交更改,添加备注信息(此时将暂存区的信息提交到本地仓库)
git push origin master 　　 # 将本地仓库的文件push到远程仓库(若 push 不成功，可加 -f 进行强推操作)
```

## 其他命令

```bash
# 查看远程连接
git remote -v 
# 删除远程连接
git remote rm origin
# 设置分支
git branch -M main
# 强制pull
git fetch --all
git reset --hard origin/master
git pull
```

ADD：配置本地用户信息只用来提交时做标识，而非用作验证，https登陆时需要手动输入用户名密码，而ssh登陆时非常easy，只要服务器端拥有公钥即可，若没公钥，则输入密码提示拒绝连接，并非密码错误。

## 遇到的问题

- 设置无误却连接不上，是因为ssh软件升级的原因，在配置文件中添加以下代码

    ```bash
    Host *
    HostkeyAlgorithms +ssh-rsa
    PubkeyAcceptedKeyTypes +ssh-rsa
    ```