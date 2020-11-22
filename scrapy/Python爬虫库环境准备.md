# 环境准备

## 1 python安装

使用anaconda方式安装，首先下载anaconda

下载地址：https://www.anaconda.com/products/individual

安装：双击安装即可

## 2  requests库安装

通过python的pip工具安装

```shell
pip3 install requests
```

## 3 selenium安装

通过Python的pip工具安装

```shell
pip3 install selenium
```

## 4 Chrome Driver

### 4.1 下载地址

https://chromedriver.storage.googleapis.com/index.html

`注`：需根据自己的google浏览器版本号选择相应的版本下载

### 4.2 环境变量配置

在windows下可以直接将下载的`chromedriver.exe`放到Python的scripts目录下

通过anaconda安装后，Scripts目录的位置为`D:\ProgramData\Anaconda3\Scripts`

## 5 phantomJS安装

PhantomJS：一个无界面的，可脚本编程的WebKit浏览器引擎

下载地址：http://phantomjs.org/download.html

API接口说明：http://phantomjs.org/api/command-line.html

安装：解压下载的压缩包，其中有一个bin目录，该目录下有一个phantomjs.exe文件，将其放到Python的Scripts目录下

## 6 aiohttp安装

一个提供异步web服务的库

通过pip安装

```
pip3 install aiohttp
```

其他

```
pip3 install cchardet aiodns
```



## 7 解析库的安装

用于在抓取网页后，从中提取信息

### 7.1 lxml安装

一个python解析库，支持HTML和xml解析

安装方式：

```
pip3 install lxml
```

### 7.2 Beautiful Soup 安装

安装方式：

```
pip3 install beautifulsoup4
```

### 7.3 pyquery安装

```
pip3 install pyquery
```

### 7.4 tesserocr安装

字符识别库

#### 7.4.1 下载tesseract

下载地址：http://digi.bib.uni-mannheim.de/tesseract

安装：双击`setup.exe`安装即可，中途可勾选`Additional languge dta(download)`选择OCR识别支持的语言包，从而使其支持多国语言

备注：语言包下载失败，原因未知

设置环境变量：将tesseract安装路径(`D:\Program Files (x86)\Tesseract-OCR`)添加到path变量中

#### 7.4.2 安装tesserocr 

```
pip3 install tesserocr pillow
```

**安装报错：**

```
error: Microsoft Visual C++ 14.0 or greater is required. Get it with "Microsoft C++ Build Tools": https://visualstudio.microsoft.com/visual-cpp-build-tools/
```

根据提示信息可知：需要Microsoft Visual C++ 14.0，

下载地址：https://visualstudio.microsoft.com/visual-cpp-build-tools/

仅下载vs_buildtools无需安装visual studio

之后再次执行`pip3 install tesserocr pillow`，出现新的错误：

```
 tesserocr.cpp(657): fatal error C1083: 无法打开包括文件: “leptonica/allheaders.h”: No such file or directory
```

百度查找原因：是因为电脑上安装了anaconda，因此需要通过anaconda安装tesserocr，命令行执行：

```shell
conda install -c simonflueckiger tesserocr pillow
```

**再次遇到错误：**

```
Solving environment: failed with initial frozen solve. Retrying with flexible solve.
Solving environment: |
Found conflicts! Looking for incompatible packages.
This can take several minutes.  Press CTRL-C to abort.
failed

UnsatisfiableError: The following specifications were found
to be incompatible with the existing python installation in your environment:

Specifications:

  - tesserocr -> python[version='>=3.5,<3.6.0a0|>=3.6,<3.7.0a0|>=3.7,<3.8.0a0']

Your python: python=3.8

If python is on the left-most side of the chain, that's the version you've asked for.
When python appears to the right, that indicates that the thing on the left is somehow
not available for the python version you are constrained to. Note that conda will not
change your python version to a different minor version unless you explicitly specify
that.
```

**原因：当前python版本为3.8.5，超过所要求的版本**

**解决：使用conda创建一个python3.6的环境，在新环境中安装依赖库**

```shell
conda create -n python36 python=3.6  #创建环境
conda activate python36  #切换环境
```

其他conda命令

```shell
conda info --envs #s查看当前有哪些环境
conda list #查看当前环境下安装了哪些包
#####################配置channel，相当于镜像源#####################
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/
conda config --set show_channel_urls yes
###############################################################

conda search fastqc #搜索特定包
conda install fastqc #安装特定包
conda install fastqc=0.11.6 #安装指定版本的包
conda install fastqc multiqc #安装多个包
conda update fastqc #更新包
conda update python #更新python、
conda update conda 
conda update anaconda #更新conda本身及anaconda元数据包
conda update fastqc --no-pin #防止某个包更新
conda remove pkg_name #删除当前环境中的某个包
conda remove -n env_name pkg_name #删除指定环境中的某个包
conda list -n env_name #查看特定环境下所有的包

conda create -n env_name #创建特定名字的环境
conda create -n env_name python=3.6 #使用特定版本的python创建环境
conda create -n env_name pandas #使用特定的包创建环境
conda env create -f environment.yaml #通过配置文件创建环境
conda env_name export > environment.yaml #导出环境配置文件
conda activate env_name #激活环境
conda deactivate env_name #停用环境
conda info --envs #查看环境
conda remove -n env_name #删除环境、
conda create --name env_clone_from --clone new_env_name #同一机器上环境复制
```



pip3安装源设置

```
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

```
C:\Users\Administrator\AppData\Roaming\pip\pip.ini
```

注`：修改pip为国内源后，pip下载速度快很多：

设置用Powershell运行conda:

（1）将anaconda的安装路径添加到环境变量

（2）conda install -n root -c pscondaenvs pscondaenvs

（3）打开powershell,执行`conda init powershell`

Powershell重新打开后出错：、

```
. : 无法加载文件 C:\Users\Administrator\Documents\WindowsPowerShell\profile.ps1，因为在此系统上禁止运行脚本。有关详细信
息，请参阅 https:/go.microsoft.com/fwlink/?LinkID=135170 中的 about_Execution_Policies。
所在位置 行:1 字符: 3
+ . 'C:\Users\Administrator\Documents\WindowsPowerShell\profile.ps1'
+   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : SecurityError: (:) []，PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess
```

解决办法：

以管理员方式打开powershell，执行以下命令：

```
set-executionpolicy remotesigned
```

重新打开后不再报错，问题解决，执行conda activate命令成功

之后找到`C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Anaconda3 (64-bit)`下的`Anaconda Powershell Prompt (Anaconda3)`文件（一个快捷方式），右键-目标（T），将其内容修改为

`%windir%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy ByPass -NoExit -Command "& 'D:\ProgramData\Anaconda3\shell\condabin\conda-hook.ps1' ; conda activate 'D:\ProgramData\Anaconda3\envs\python36' "`最后一个路径为要设置的每次启动时，默认进入的conda环境

之后将这个快捷方式固定到任务栏

## 8 数据库的安装

### 8.1 Mysql数据库安装

下载地址：https://www.mysql.com/cn/downloads

中文教程：http://www.runoob.com/mysql/mysql-tutorial.html

安装过程参考：https://blog.csdn.net/weixin_42869365/article/details/83472466

常用命令：

```
net start mysql #启动mysql服务
mysql -u root -p #登陆
mysqladmin -u root -p password #设置密码
exit #退出
```

设置mysql服务启动方式：

搜索service.msc 找到mysql，设置启动方式为自动或手动



### 8.2  MonoDB安装

官方网站：https://www.mongodb.com

中文教程：http://www.runoob.com/mongodb/mongodb-tutorial.html

安装：下载.msi版本安装包安装

### 8.3 Redis安装

官方网站：https://redis.io

官方文档：https://redies.io/documentation

中文教程：http://www.runoob.com/redis/redis-tutorial.html

Redis Desktop Manager GitHub: https://github.com/uglide/RedisDesktopManager

Github下安装包下载链接：https://github.com/MsOpenTech/redis/releases

## 9 安装存储库

### 9.1 PyMsyql安装

```
pip3 install pymysql
```

9.2 mongo

```
pip3 install pymongo
```

9.3 redis

```
pip3 instsall redis
```

### 9.4 redisDump安装

一个用于redis数据导入导出的工具

官方文档：http://delanotes.com/redis-dump

9.4.1 相关链接

Github:https://github.com/delano/redis-dump

官方文档: http://delanotes.com/redis-dump

9.4.2 安装Ruby

参考：http://www.ruby-lang.org/zh_cn/documentation/installation

需要选择 [Ruby+Devkit ](https://github.com/oneclick/rubyinstaller2/releases/download/RubyInstaller-2.7.2-1/rubyinstaller-devkit-2.7.2-1-x86.exe)版本的ruby-installer安装ruby，否则之后安装redis-dump会失败.

redis-dump安装成功信息

```
(python36) PS C:\Users\Administrator> gem install redis-dump
Temporarily enhancing PATH for MSYS/MINGW...
Building native extensions. This could take a while...
Successfully installed yajl-ruby-1.4.1
Successfully installed redis-dump-0.4.0
Parsing documentation for yajl-ruby-1.4.1
Installing ri documentation for yajl-ruby-1.4.1
Parsing documentation for redis-dump-0.4.0
Installing ri documentation for redis-dump-0.4.0
Done installing documentation for yajl-ruby, redis-dump after 0 seconds
```

9.4.3使用gem安装redis-dump

```
gem install redis-dump
```

最后执行`redis-dump`和`redis-load`命令，若命令可以执行则说明安装成功

## 10 Web库的安装

10.1 flask库

10.1.1 相关链接

Github: https://github.com/pallets/flask

官方文档：http://flask.pocoo.org

中文文档：http://docs.jinkan.org/docs/flask

PyPI: https://pypi.python.org/pypi/flask

10.1.2 安装

```
pip3 install flask
```

10.2 Tornado

```
pip3 install tornado
```

## 11  web 爬取相关库的安装

官方网站：https://www.charlesproxy.com

下载链接：https://www.charlesproxy.com/download



## 12  docker 安装

https://docs.docker.com/docker-for-windows/install



## 其他

安装vim并在powershell中使用

参考https://blog.csdn.net/qq_37933114/article/details/82932840



