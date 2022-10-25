## 租服务器

- 宽带拉满

## 配置服务器

- 修改实例名称  >> 类型、用途 、到期时间

- 修改实例 root 用户密码

- 使用root账户登录远程主机

    ```bash
    ssh root@主机ip
    ```

- 安装sudo、创建普通用户、 给普通用户分配sudo权限、切换到普通用户

    ```bash
    apt update
    useradd -d /home/fanfan -m fanfan
    passwd fanfan
    usermod -aG sudo fanfan
    su fanfan
    ```

- 安装ssh、vim、tmux、tree、zsh、curl、git

- 配置ssh免密登录，配置vim、tmux、zsh

- 安装 Docker
