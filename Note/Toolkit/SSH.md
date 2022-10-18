## 服务端

### Linux安装并启动SSH

```bash
# 安装ssh服务
sudo apt-get install openssh-server
# 启动ssh服务
sudo /etc/init.d/ssh start
# 设置开机自启动
sudo systemctl enable ssh
# 关闭ssh开机自动启动命令
sudo systemctl disable ssh
# 单次开启ssh
sudo systemctl start ssh
# 单次关闭ssh
sudo systemctl stop ssh
# 设置好后重启
reboot
```

## 客户端

### 生成密钥对

```bash
ssh-keygen # 生成密钥(~/.ssh内)
```

### 给服务器起别名

本地 **.ssh**文件下新建文件**config**并写入以下内容

```bash
Host 别名
    HostName 服务器IP
    User  登录用户名
	Port  端口号(默认22可不写)
```

### 配置免密登录

上传本地公钥即可！！！

- 方式一：命令行上传

    - linux：ssh-copy-id username@IP / HostName别名
    - Windows：无法识别该命令，先写个函数再上传

    ```bash
    function ssh-copy-id([string]$userAtMachine, $args){   
         $publicKey = "$ENV:USERPROFILE" + "/.ssh/id_rsa.pub"
         if (!(Test-Path "$publicKey")){
            Write-Error "ERROR: failed to open ID file '$publicKey': No such file"            
         }
         else {
             & cat "$publicKey" | ssh $args $userAtMachine "umask 077; test -d .ssh || mkdir .ssh ; cat >> .ssh/authorized_keys || exit 1"      
        }
    }
    ```

- 方式二：手动上传

    - 在用户主目录下，如用户名`wenzhu`，则在`/home/wenzhu`目录下新建一个`.ssh`(*注意前面有个点*)
    - 修改`.ssh`文件夹的权限为700 `chmod 700 .ssh`
    - 新建名为`authorized_keys`的文件，修改权限为600 `chmod 600 authorized_keys`
    - 将本地PC生成的公钥文件的内容复制到`authorized_keys`后面，这样就算配置完成了。
    - 如果有新的PC需要连接该git服务器，按照步骤1生成公私钥，只需要将公钥复制到`authorized_keys`就可以了

## 其他命令

```bash
# 重启ssh服务
service ssh restart
```

## 问题

> WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!

>  解决办法：ssh-keygen -R 服务器IP  + ssh -p 22 root@服务器IP