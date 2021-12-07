## <div align="center">Docker</div>
<details open>
<summary>docker配置</summary>
安装docker
  
```bash
## 官方安装
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
## 国内安装
curl -sSL https://get.daocloud.io/docker | sh
```
</details>

<details open>
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

## <div align="center">NVIDIA</div>
<details open>
<summary>nvidia配置</summary>
安装nvidia驱动
  
```bash
## 查看最新驱动
ubuntu-drivers devices
## 安装驱动
sudo apt-get install nvidia-driver-470  ## 可选择最新版本
```
</details>
