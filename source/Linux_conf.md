# Linux配置
## 更换Ubuntu源
### step 1: 首先看看国内有哪些源

>Win10 Ubuntu子系统路径：`%USERNAME%\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\rootfs`

名称 | 域名 
:-: | :-: 
阿里|`http://mirrors.aliyun.com/ubuntu/`
163|`http://mirrors.163.com/ubuntu/`
中科大|`https://mirrors.ustc.edu.cn/ubuntu/`
清华|`http://mirrors.tuna.tsinghua.edu.cn/ubuntu/`
电子科大|`http://ubuntu.dormforce.net/ubuntu/`

### step 2: 获取 Ubuntu 代号

`lsb_release -a`

Ubuntu 18.04.1，查出来的代号就是 bionic.

### step 3: 编辑源

![](https://img-blog.csdnimg.cn/20190121012630368.png)

红色边框：服务器地址
紫色边框：Ubuntu 的代号（Codename）

### step 4: 修改源文件 sources.list
先备份

`sudo cp /etc/apt/sources.list /etc/apt/sources.list.bcakup`

再修改（如改为163源）
```
#163源
deb http://mirrors.163.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ bionic-proposed main restricted universe multiverse

##測試版源
deb http://mirrors.163.com/ubuntu/ bionic-backports main restricted universe multiverse

# 源碼
deb-src http://mirrors.163.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ bionic-proposed main restricted universe multiverse

##測試版源
deb-src http://mirrors.163.com/ubuntu/ bionic-backports main restricted universe multiverse
```

### step 5: 更新软件列表和升级
更新软件列表（检测出可更新的软件）：

`sudo apt-get update`

更新软件：

`sudo apt-get upgrade`

## 安装Python3、pip

```bash
# 安装python3
sudo apt install python3
# 安装pip
sudo apt install python3-pip
```

### 更换pip源

pip国内的一些镜像


| 名称 | 域名 |
| :-: | :-: |
|阿里云 |https://mirrors.aliyun.com/pypi/simple/|
|中国科技大学| https://pypi.mirrors.ustc.edu.cn/simple/|
|清华大学| https://pypi.tuna.tsinghua.edu.cn/simple/|

修改 ~/.pip/pip.conf (没有就创建一个)， 内容如下：

```
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
trusted-host=mirrors.aliyun.com
```

