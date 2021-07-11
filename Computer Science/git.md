# GIT
## linux 安装
[安装git](https://blog.csdn.net/qq_28903377/article/details/86148687)
```linux```
sudo yum groupinstall "Development Tools"

sudo yum install wget unzip gettext-devel openssl-devel perl-CPAN perl-devel zlib-devel libcurl-devel expat-devel

cd 到git的目录下

sudo make prefix=/usr/local/bin all

sudo make prefix=/usr/local/git install

sudo echo "export PATH=$PATH:/usr/local/git/bin" >> /etc/profile

sudo chomd 777 /etc/profile

sudo source /etc/profile

git --version
```

