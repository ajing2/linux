### memcache和memcached在php中的应用
* **memcache在php中编译** 
``` daf
wget http://www.lishiming.net/data/attachment/forum/memcache-2.2.3.tgz
 tar zxvf memcache-2.2.3.tgz
cd memcache-2.2.3
/export/servers/php/bin/phpize
./configure --with-php-config=/usr/local/php/bin/php-config
make
 make install
mkdir -p /export/servers/php/ext
cp modules/memcache.so /export/servers/php/ext/  #把memcache.so 拷贝至php的extension_dir下
```  

查看php extension_dir的方法是  /export/servers/php/bin/php -i |grep extension_dir  
修改扩展路径，在php.ini中修改：  
extension_dir = "/usr/local/php/ext"  
然后在php.ini 中添加  
extension = memcache.so  

保存后可以利用 /usr/local/php/bin/php -m |grep memcache 检测和查看具体的参数  


* **memcached 的编译安装**  
```
wget http://syslab.comsenz.com/downloads/linux/memcached-1.4.5.tar.gz
tar zxvf memcached-1.2.8.tar.gz
cd  memcached-1.2.8
./configure --prefix=/export/servers/memcached
make && make install
```
启动：  
/export/servers/memcached/bin/memcached -m 2048 -p 11211 -l 127.0.0.1 -d -u www  
-m  后边指定memecached使用多少内存，单位是M  
-p  指定memcached 启动端口  
-l  指定绑定的IP  
-u  指定以某个账户的身份启动  

* **php 添加 redis 扩展模块**  
下载地址：
[redis-2.2.5.tgz](http://pecl.php.net/get/redis-2.2.5.tgz)
```
tar zxf redis-2.2.5.tgz -C ../
cd ../redis-2.2.5/
/export/servers/php/bin/phpize
Configuring for:
PHP Api Version: 20100412
Zend Module Api No: 20100525
Zend Extension Api No: 220100525
 ./configure --with-php-config=/export/servers/php/bin/php-config
make&&make install
cp modules/redis.so /export/servers/php/ext/
```  

```vim /usr/local/php/php.ini```
extension_dir = /
extension = redis.so

```/usr/local/php/bin/php -m | grep redis```
redis
