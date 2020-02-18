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
├ LICENSE
├ Makefile
├ README.md
├ make.bat
└ source
    ├ _static
    ├ _templates
    ├ conf.py
    └ index.rst
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
extensions = [
        'recommonmark',
        'sphinx_markdown_tables',
]

html_theme = 'sphinx_rtd_theme'
```

添加`./requirements.txt` pip要求文件（**Readthedocs配置**时需要用到）

```text
# markdown suport
recommonmark
# markdown table suport
sphinx-markdown-tables

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
   :caption: 目录:
   
   contents
```

创建`./source/contents.rst`文件

```rst
.. toctree::
   :maxdepth: 2
   :caption: 目录

   test
```

创建`./source/test.md`文件

```md
# here is a test markdown file
```

然后同步到Github


