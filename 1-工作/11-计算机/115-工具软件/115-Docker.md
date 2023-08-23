# Docker

## 安装
### 2022/9/22
参考文章：[Ubuntu 20.04安装Docker](https://www.cnblogs.com/Can-daydayup/p/16472375.html)
注：使用阿里镜像源

```bash
# 更新 apt 包索引
sudo apt-get update
# 安装必备的软件包以允许apt通过 HTTPS 
sudo apt-get install ca-certificates curl gnupg lsb-release
# 使用存储库（repository）添加阿里云的GPG密钥
curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
# 设置存储库
sudo add-apt-repository "deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
# 再次更新
sudo apt-get update
# 安装 Docker
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
docker version # 验证安装是否成功
systemctl status docker # 验证 Docker 服务是否在运行
sudo systemctl start docker # 启动Docker服务
```

## 基础操作
参考资料：[Docker基本操作](https://blog.csdn.net/m0_37714245/article/details/81713477)

docker 的启动与停止
* 启动：`systemctl start docker`
* 停止：`systemctl stop docker`
* 重启：`systemctl restart docker`
* 查看状态：`systemctl status docker`
* 开机启动：`systemctl enable docker`

镜像（image）
* 列出镜像：`docker image ls -a`
* 【？】拉取镜像：`docker image pull library/hello-world`
* 删除镜像：`docker image rm 镜像名或镜像id`

完整的镜像名为`REPOSITORY:TAG`，例如`oslab:2021`
* 一个 REPOSITORY 可以有多个 TAG

容器（container）
* 创建容器：`docker run [选项] 镜像名 [向容器中传入的命令]`
	- `-itd`，i 表示交互模式，t 表示进入终端，d 表示后台运行容器，并返回容器ID
	- `--name 容器名称`：指定容器名称
	- `-v 本地目录:容器目录`：将本地目录挂载到容器中
	- `-p 主机端口:容器端口`：将容器的端口绑定到主机的端口上（可以实现远程连接直接连接 docker 容器）
* 进入已运行的容器：`docker exec -it 容器名或容器id 进入后执行的第一个命令`
	- 第一个命令：如`bash`
* 查看容器：`docker container ls [--all]`
* 停止容器：`docker container stop 容器名或容器id`
* 启动容器：`docker container start 容器名或容器id`
* kill 容器：`docker container kill 容器名或容器id`
	- kill 相比于 stop 更粗暴，重新 start 后进程号会改变
* 删除容器：`docker container rm 容器名或容器id`

保存相关
* 将容器保存为镜像：`docker commit 容器名 镜像名`
* 将镜像保存为文件：`docker save -o 保存的文件名 镜像名`
* 加载镜像：`docker load -i 文件名`或`docker load < 文件名`

## 直接远程连接到 Docker
参考教程：[【docker】VScode连接远程服务器上的docker容器并使用jupyterlab](https://blog.csdn.net/u011119817/article/details/115966917)
参考教程2：[Docker学习之SSH连接docker容器](https://cloud.tencent.com/developer/article/1550935)

注意：应该按照教程 2 修改 sshd_config 文件，然后重启服务应该用教程 1 中的 `/etc/init.d/ssh restart`

注：约定自己所用远程服务器，用来连接 docker 的端口号为 8080 到 8089

容器中原来没有 ssh，新安装的可能找不到 sshd 服务：[解决更新ssh后在/etc/init.d下无sshd的问题](https://www.cnblogs.com/ninicwang/p/10512155.html)

## 镜像加速器
> sudo mkdir -p /etc/docker
> sudo tee /etc/docker/daemon.json <<-'EOF'
> {
>   "registry-mirrors": ["https://d1naqwca.mirror.aliyuncs.com"]
> }
> EOF
> sudo systemctl daemon-reload
> sudo systemctl restart docker

## 我的 Docker 容器
### julycf
July 的 Codefield

image：ubuntu

安装如下内容：
* openssh-server, openssh-client, ssh
* software-properties-common (PPA)
* nvim
* gcc, g++, cmake
* git
* opencv（自己编译）
* vscode-server（VSC 自己安装）
