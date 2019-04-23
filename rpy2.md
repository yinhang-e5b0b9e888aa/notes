# rpy2

## CentOS 7上面安装步骤

1. yum install centos-release-scl
2. yum install devtoolset-7-gcc-c++
3. scl enable devtoolset-7 bash
4. yum install R
5. conda install gcc_linux-64
6. conda install -c r rpy2=2.9.4
7. conda install tzlocal
8. ~/.Rprofile中加入如下内容：
   options("repos" = c(CRAN="https://mirrors.tuna.tsinghua.edu.cn/CRAN/"))
9. R中安装mice:
   install.packages("mice")
   
1. 系统的gcc最好安装最新版本（对应上面1.2.3步）
2. conda自带的gcc最好也是最新版本（对应上面5步）
3. 安装过程中可能出现网络断开，需要看安装过程，即使最后显示成功安装，也不一定，需要重新执行安装
4. rpy2需要通过conda安装，并且指定为2.9.4版本，新版本与这个版本不兼容
5. rpy2安装成功之后才去R语言中安装mice
