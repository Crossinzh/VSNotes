
---
### Ubuntu 百度输入法乱码问题
Ubuntu 20.04下百度输入法候选词乱码的情况，是因为没有安装QT造成的。

**修复方法：**
> sudo apt install qt5-default qtcreator qml-module-qtquick-controls2

---

### Linux 修改 python 版本

查看python位置：```whereis python```
<div align=center><img src="images/Screenshot from 2021-12-25 09-49-46.png"></div>

```which python``` which命令用于查找文件。which指令会在环境变量$PATH设置的目录里查找符合条件的文件。
<div align=center><img src="images/Screenshot from 2021-12-25 09-51-02.png"></div>

查看python版本：```python --version```

查看linux系统当前已经安装那几个python版本：```ll /usr/bin/pyth*```
注：ll（查看文件及目录详情）
<div align=center><img src="images/Screenshot from 2021-12-25 09-55-13.png"></div>

**更改python版本步骤**
```which python``` 
查找目录
```cd /usr/bin```
切换至目录
```rm -rf python```
删除python软连接文件
```ln -s /usr/bin/python3 python```
重新创建新指向python
```python --version```
查看python版本

<div align=center><img src="images/Screenshot from 2021-12-25 10-25-42.png"></div>

---

### Bazel 安装

1. 在安装Bazel之前需要先安装JDK8。
```sudo apt-get install openjdk-8-jdk```
如若JDK8安装成功，java命令执行后会打印出一些相关的命令语法。
```java```
```java -version```打印出JDK的版本

2.  JDK8安装之后还要继续安装 Bazel 的其他依赖工具包。
安装先决条件：pkg-config, zip, g++, zliblg-dev, unzip, python3

```sudo apt-get install pkg-config zip g++ zliblg-dev unzip python3```或
```sudo apt-get install pkg-config zip g++ zliblg-dev unzip ```

3.  下载Bazel
从GitHub上的[Bazel发行页面](https://github.com/bazelbuild/bazel/releases)下载Bazel二进制安装程序。(bazel-\<version>-installer-linux-x86_64.sh)

4.  运行安装程序

先修改权限：
```chmod +x bazel-<version>-installer-linux-x86_64.sh```
<div align=center><img src="images/Screenshot from 2021-12-26 04-53-59.png"></div>

然后运行Bazel安装程序：
```./bazel-<version>-installer-linux-x86_64.sh --user```
<div align=center><img src="images/Screenshot from 2021-12-26 04-56-35.png"></div>
--user标志将Bazel安装到$HOME/bin系统上的目录并设置.bazelrc路径$HOME/.bazelrc。使用--help命令可以查看其他安装选项。

查看 /home/xxx/bin
<div align=center><img src="images/Screenshot from 2021-12-26 05-00-26.png"></div>

5.  设置环境
使用--user上面的标志运行Bazel安装程序，则Bazel可执行文件将安装在$HOME/bin目录中，将此目录添加到默认路径。输入bazel命令验证其是否安装成功。

```export PATH="$PATH:$HOME/bin"```
```bazel```

<div align=center><img src="images/Screenshot from 2021-12-26 05-06-09.png"></div>

---
