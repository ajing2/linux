# PHP安装
### 声明
在安装php的时候，一定要先安装mysql和httpd，因为在编译php时候，要制定mysql和httpd的路径。否则就会报错

![image](http://note.youdao.com/yws/public/resource/cc2c288abae1da4d38a60ae30f822532/xmlnote/652EE89F0680405FAD9F4BF16764CF40/6407)

### 下载php

**安装php之前，请提前安装好其所依赖的安装包：**

    yum install -y  bzip2-devel curl-devel db4-devel libjpeg-devel libpng-devel libXpm-devel gmp-devel libc-client-devel openldap-devel unixODBC-devel postgresql-devel sqlite-devel aspell-devel  net-snmp-devel libxslt-devel libxml2-devel pcre-devel mysql-devel unixODBC-devel postgresql-devel pspell-devel net-snmp-devel
    
    wget  http://cn2.php.net/distributions/php-5.5.38.tar.gz
    cd /usr/local/src
    tar xzvf php-5.5.38.tar.gz
    cd php-5.5.38
    ./configure   --prefix=/export/servers/php   --with-apxs2=/export/servers/apache2/bin/apxs   --with-config-file-path=/export/servers/php/etc   --with-mysql=/export/servers/mysql   --with-libxml-dir   --with-gd   --with-jpeg-dir   --with-png-dir   --with-freetype-dir   --with-iconv-dir   --with-zlib-dir   --with-bz2   --with-openssl   --with-mcrypt   --enable-soap   --enable-gd-native-ttf   --enable-mbstring   --enable-sockets   --enable-exif   --disable-ipv6 
    
    
![image](http://note.youdao.com/yws/public/resource/cc2c288abae1da4d38a60ae30f822532/xmlnote/C2F65EB961C94CF4A8134EAD4353C118/5609)

```make && make install```

**注意：**
因为centos6.x 默认的yum源没有libmcrypt-devel 这个包，只能借助第三方yum源。


可以百度下载一个，


rpm -ivh "http://www.aminglinux.com/bbs/data/attachment/forum/month_1211/epel-release-6-7.noarch.rpm"

yum install -y  libmcrypt-devel


或者网上搜一个libmcrypt-devel的源码包，自己编译安装，
推荐百度搜索findrpm      然后在网站内搜索包名


