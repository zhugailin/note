## <div align="center">Docker</div>
<details close>
<summary>docker配置</summary>
安装docker
  
```bash
## 官方安装
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
## 国内安装
curl -sSL https://get.daocloud.io/docker | sh
```
</details>

<details close>
<summary>加入docker组</summary>
使用docker时不用sudo
  
```bash
## 添加docker组
sudo groupadd docker
## 用户添加到docker组
sudo gpasswd -a ${USER} docker
## 重启docker
sudo service docker restart
## 退出shell重新进入就完成了。
```
</details>

<details close>
<summary>docker操作</summary>
配置镜像
  
```bash
## 下载镜像
docker pull ultralytics/yolov5:v5.0
## 镜像提交更改
docker commit -a "yh_test" -m "build detectron2 develop" bc94bd5dc434  yh/dnn:ub18-cuda11.1-conda-trt7.2
## 打包镜像
docker save -o yh_dnn.tar yh/dnn:ub18-cuda11.1-conda-trt7.2
本地载入镜像
docker load --input yh_dnn.tar
```
常用命令

```bash
docker images # 查看所有镜像
docker run # 运行docker
docker ps # 查看正在运行的docker
docker attach # 加入运行中的镜像
docker stop # 停止正在运行的镜像
docker start # 开始运行镜像
Ctrl+P+Q # 退出容器
## 开机自启动docker
docker update --restart=always yh_inspection
```
docker run 命令

```bash
docker run 
    -it \  # 必须
    --gpus '"device=0,1"' \ # 使用gpu
    --name "yh_test" \ # 命名
    -p 8042:22 \ # 端口映射
    --ipc=host \
    -v /home/yh/image:/home/yh/image \ # 文件夹映射
    -e LANG=C.UTF-8 -e LC_ALL=C.UTF-8 \ # 改编码格式
    yh/dnn:ub18-cuda11.1-conda-trt7.2 /bin/bash
```
docker内部配置ssh映射

```bash
mkdir /var/run/sshd
echo 'root:Yuan930216' | chpasswd
sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
echo "export VISIBLE=now" >> /etc/profile
service ssh restart
```
</details>

## <div align="center">NVIDIA</div>
<details close>
<summary>nvidia配置</summary>
安装nvidia驱动
  
```bash
## 查看最新驱动
ubuntu-drivers devices
## 安装驱动
sudo apt-get install nvidia-driver-470  ## 可选择最新版本
## 重启生效
```
安装docker需要的--gpu插件
  
``` bash
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit
sudo systemctl restart docker
```
</details>

## <div align="center">GIT</div>
<details close>
<summary>git命令</summary>
git常用命令
  
```bash
git commit -m "" # 提交更新 
## 新建分支并 进入分支
{git branch bugFix; git checkout bagFix; git commit} = {git checkout -b bugFix}
git merge bugFix # 合并分支
git rebase main # 顺序合并分支
## 移动HEAD
git checkout HEAD^ ;  git checkout HEAD~4 ; git branch -f main HEAD~3
## 从远程仓库提取数据
git fetch # 将log提取下来，本地库代码不变
## 直接更新本地库
git pull = {git fetch; git merge o/main)
## 远程库添加伪提交
git fakeTeamwork foo 3
```
git 实练命令
  
```bash
git tag \ # 查看tag
    --contains 11528ce083dc9ff83ee3a8f908  # 查看包含此提交的tag
git stash # 暂存
```
</details>

## <div align="center">杂烩</div>
screen的使用
  
```bash
screen
    -ls # 查看存在的screen
    -dms  yh_test # 创建screen
    -r yh_test # 加入screen
    exit # 退出并删除screen
```
rsync,不同服务器之间目录同步

```bash
rsync -r -K --delete /dataset/uploading_data/ yuanhui@172.26.12.14:/dataset/uploading_data/
```
vim常用命令

```bash
nyy/P # 复制粘贴
## 搜索关键词
/user  # 表示搜索user
## 替换关键字
:n,$s/vivian/sky/g # 替换第 n 行开始到最后一行中每一行所有 vivian 为 sky
```
查看cpu

```bash
## 查看逻辑核数量
cat /proc/cpuinfo| grep "processor"| wc -l
## 查看物理核数量
cat /proc/cpuinfo| grep "physical id"| sort| uniq| wc -l
```

