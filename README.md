# Sphinx_GitHub_ReadtheDocs

[![Documentation Status](https://readthedocs.org/projects/sphinx-github-readthedocstsanfer/badge/?version=latest)](https://sphinx-github-readthedocstsanfer.readthedocs.io/zh_CN/latest/?badge=latest)

创建Sphinx + GitHub + ReadtheDocs托管文档

# Linux配置
## 更换Ubuntu源
### step 1: 首先看看国内有哪些源


|   名称   |                     域名                      |
| :------: | :-------------------------------------------: |
|   阿里   |      `http://mirrors.aliyun.com/ubuntu/`      |
|   163    |       `http://mirrors.163.com/ubuntu/`        |
|  中科大  |     `https://mirrors.ustc.edu.cn/ubuntu/`     |
|   清华   | `http://mirrors.tuna.tsinghua.edu.cn/ubuntu/` |
| 电子科大 |     `http://ubuntu.dormforce.net/ubuntu/`     |

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

`sudo apt update`

更新软件：

`sudo apt upgrade`

## 安装Python3、pip

```bash
# 安装python3
sudo apt install python3
# 安装pip
sudo apt install python3-pip
```

### 更换pip源

pip国内的一些镜像


|     名称     |                   域名                    |
| :----------: | :---------------------------------------: |
|    阿里云    |  https://mirrors.aliyun.com/pypi/simple/  |
| 中国科技大学 | https://pypi.mirrors.ustc.edu.cn/simple/  |
|   清华大学   | https://pypi.tuna.tsinghua.edu.cn/simple/ |

修改 ~/.pip/pip.conf (没有就创建一个)， 内容如下：

```
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
trusted-host=mirrors.aliyun.com
```



# Github配置

克隆一个新的公共的空白仓库到本地 `~\Sphinx_GitHub_ReadtheDocs`

目录结构：

```sh
.
├── LICENSE
└── README.md
```



# Sphinx配置

## 安装Sphinx、及其插件

```bash
pip3 install sphinx sphinx_rtd_theme recommonmark sphinx-markdown-tables
```

## 初始化Sphinx

```sh
# 进入Git根目录
cd ~/Sphinx_GitHub_ReadtheDocs
# 开始快速配置sphinx
sphinx-quickstart

# 选择把源文件和删除文件分开（y）
> Separate source and build directories (y/n) [n]:y
# 项目名称
> Project name: Sphinx_GitHub_ReadtheDocs
# 作者姓名
> Author name(s): Tsanfer
# 版本号
> Project release []: 0.2
# 语言
> Project language [en]: zh_CN
```

目录结构：

```sh
.
├── LICENSE
├── Makefile
├── README.md
├── make.bat
└── source
    ├── _static
    ├── _templates
    ├── conf.py
    └── index.rst
```

验证配置是否正确：

```sh
cd ~/work/scrapy-cookbook
make html
```

浏览器打开`./build/index.html`查看


## 配置Sphinx主题，插件

配置`./source/conf.py`配置文件：

```python
# -- General configuration ---------------------------------------------------

# Add any Sphinx extension module names here, as strings. They can be
# extensions coming with Sphinx (named 'sphinx.ext.*') or your custom
# ones.

extensions = [
        'recommonmark',
        'sphinx_markdown_tables',
        'sphinxemoji.sphinxemoji',
]

# -- Options for HTML output -------------------------------------------------

# The theme to use for HTML and HTML Help pages.  See the documentation for
# a list of builtin themes.
#
html_theme = 'sphinx_rtd_theme'

# The master toctree document.
master_doc = 'index'
```

添加`./requirements.txt` pip要求文件（**Readthedocs配置**时需要用到）

```text
# markdown suport
recommonmark
# markdown table suport
sphinx-markdown-tables
#emoji
sphinxemoji

# theme default rtd

# crate-docs-theme
sphinx-rtd-theme
```

## 更改标题，添加目录，添加文件

配置`./source/index.rst`文件：

```rst
创建Sphinx + GitHub + ReadtheDocs托管文档
=====================================================

.. toctree::
   :maxdepth: 2
   :numbered:
   
   Sphinx_GitHub_ReadtheDocs
```

创建`./source/Sphinx_GitHub_ReadtheDocs.md`文件

```
# here is a test markdown file
```

然后同步到Github



# Readthedocs配置

导入代码库:
![](https://i.loli.net/2020/02/18/OvZl5xmkRyiWn1U.png)

指定pip要求文件: `./requirements.txt`
![](https://i.loli.net/2020/02/18/FbK8JTxoN72M5G9.png)
