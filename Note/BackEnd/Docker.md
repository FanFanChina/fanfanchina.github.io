# Docker

# 简介

Docker安装在服务器上，包含多个镜像，Docker可以把一个镜像分出多个相同的容器，容器可以看成一个个小的服务器

镜像和容器的关系可以看成为类和对象的关系

Docker迁移十分的简单！！！

# 安装

[Docker 乌班图安装](https://docs.docker.com/engine/install/ubuntu/)（尽量在Tumx里面运行，防止意外关闭终端后，工作进度丢失）

翻到 ****Install using the repository 复制安装代码即可****

# Docker教程

## 省去sudo

为了避免每次使用docker命令都需要加上sudo权限，可以将当前用户加入安装中自动创建的docker用户组

执行完此操作后，**需要退出服务器，再重新登录回来**，才可以省去sudo权限。

```bash
sudo usermod -aG docker $USER
```

## 镜像命令

### 拉取镜像

```bash
镜像构成 —— 名字:版本号
docker pull ubuntu:20.04：# 拉取一个镜像
```

### 列出本地所有镜像

```bash
docker images：# 列出本地所有镜像
```

### 删除镜像

```bash
docker image rm ubuntu:20.04
docker rmi ubuntu:20.04：
```

### 导出镜像

```bash
docker [container] commit CONTAINER IMAGE_NAME:TAG：# 创建某个container的镜像
```

### 导入镜像

```bash
docker load -i ubuntu_20_04.tar # 将镜像ubuntu:20.04从本地文件ubuntu_20_04.tar中加载出来
```

## 容器命令

### 创建容器

```bash
docker [container] create -it ubuntu:20.04：# 利用镜像ubuntu:20.04创建一个容器
docker [contaienr] run -itd ubuntu:20.04：  # 创建并启动一个容器
```

### 删除容器

```bash
docker [container] rm CONTAINER # 删除容器
docker container prune # 删除所有已停止的容器
```

### 查看容器

```bash
docker ps -a：# 查看本地的所有容器
docker ps # 查看本地正在运行的容器
```

### 修改容器属性

```bash
docker rename CONTAINER1 CONTAINER2 # 重命名容器
docker update CONTAINER --memory 500MB # 修改容器限制
```

### 启动、关闭、重启容器

```bash
docker [container] start CONTAINER：# 启动容器
docker [container] stop CONTAINER：# 停止容器
docker [container] restart CONTAINER：# 重启容器
```

### 进入容器

```bash
docker [container] attach CONTAINER：# 进入容器
```

### 退出容器

```bash
ctrl + p and ctrl q # 退出但不关闭该容器
strl + d # 退出并关闭该容器
```

### 在容器里执行命令

```bash
docker [container] exec CONTAINER COMMAND # 在容器中执行命令
```

### 导出容器的镜像

```bash
docker export -o xxx.tar CONTAINER # 将容器CONTAINER导出到本地文件xxx.tar中
```

### 导入容器的镜像

```bash
docker import xxx.tar image_name #将本地文件xxx.tar导入成镜像，并将镜像命名为image_name
```

> 容器导出的是他的模板镜像而非本身
> 

> docker export/import 与 docker save/load的区别
export/import会丢弃历史记录和元数据信息，仅保存容器当时的快照状态
save/load会保存完整记录，体积更大
> 

### 容器和本地文件传送

```bash
docker cp xxx CONTAINER:xxx 或 docker cp CONTAINER:xxx xxx：# 在本地和容器间复制文件
```

### 容器添加端口

- 创建时添加：docker run -p 20000:22 -p 8000:8000 --name test -itd ubuntu:20.04
- 已经生成的容器无法添加端口，可以先转为镜像，然后重新生成容器

### 其他命令

```bash
docker top CONTAINER # 查看某个容器内的所有进程
docker stats # 查看所有容器的统计信息，包括CPU、内存、存储、网络等信息
```