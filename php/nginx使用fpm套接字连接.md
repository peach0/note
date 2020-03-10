一般默认搭建环境时，都是使用

```bash
fastcgi_pass 127.0.0.1:9000;
```

来连接php-fpm，通过查找资料得知，php在5.3之后的版本，如果在php-fpm的conf里默认是

```bash
listen = 127.0.0.1:9000;
```

则不会生成php-fpm.sock，所以在配置nginx的配置文件时，也就无法通过socket来连接php-fpm。

所以只要将默认的listen配置改一下就可以(**注意权限**)。

记录下自己操作的步骤：

- 查找php-fpm的配置文件在哪儿

  ```bash
  php -i |grep config --color
  
  '--with-config-file-path=/etc
  ```

- 确认都有哪些配置文件

  ```bash
  atinosun@localhost environment $ ls /etc/php*
  /etc/php-fpm.conf		/etc/php-fpm.conf.default	/etc/php.ini.default		/etc/php.ini.default-previous
  
  /etc/php-fpm.d:
  www.conf		www.conf.default
  ```

- 更改fpm的配置

  ```
   vi /etc/php-fpm.d/www.conf
  ```

   - 更改 权限，将用户和用户组都更改为nginx使用的

     ```
     ; Unix user/group of processes
     ; Note: The user is mandatory. If the group is not set, the default user's group
     ;       will be used.
     user = nobody
     group = nobody
     ```

     

   - 打开注释

     ```bash
     ; Set permissions for unix socket, if one is used. In Linux, read/write
     ; permissions must be set in order to allow connections from a web server. Many
     ; BSD-derived systems allow connections regardless of permissions.
     ; Default Values: user and group are set as the running user
     ;                 mode is set to 0660
     listen.owner = nobody
     listen.group = nobody
     listen.mode = 0660
     ```

  - 更改监听模式

    ```bash
    ; The address on which to accept FastCGI requests.
    ; Valid syntaxes are:
    ;   'ip.add.re.ss:port'    - to listen on a TCP socket to a specific IPv4 address on
    ;                            a specific port;
    ;   '[ip:6:addr:ess]:port' - to listen on a TCP socket to a specific IPv6 address on
    ;                            a specific port;
    ;   'port'                 - to listen on a TCP socket to all addresses
    ;                            (IPv6 and IPv4-mapped) on a specific port;
    ;   '/path/to/unix/socket' - to listen on a unix socket.
    ; Note: This value is mandatory.
    ;listen = 127.0.0.1:9000
    listen = '/Users/atinosun/environment/php-fpm.sock'
    ```

- 重启php-fpm

  ```
  atinosun@localhost php-fpm.d $ ps aux|grep fpm
  atinosun         90552   0.0  0.0  4268020    780 s002  S+    8:20PM   0:00.00 grep fpm
  nobody           90108   0.0  0.0  4310664    200   ??  S     8:00PM   0:00.00 php-fpm
  nobody           90107   0.0  0.0  4310664   1364   ??  S     8:00PM   0:00.01 php-fpm
  root             90106   0.0  0.0  4310664    384   ??  Ss    8:00PM   0:00.04 php-fpm
  atinosun@localhost php-fpm.d $ sudo kill -9 90108 90107 90106
  Password:
  atinosun@localhost php-fpm.d $ sudo php-fpm
  ```

   - 此时已经可以在配置的socket地址处看到生成了socket

     ```bash
     atinosun@localhost environment $ ll
     total 0
     drwxr-xr-x@  5 atinosun  staff    160 Mar 17 20:20 ./
     drwxr-xr-x@ 32 atinosun  staff   1024 Mar 17 20:19 ../
     drwxrwxr-x@  5 atinosun  staff    160 Aug  1  2018 log/
     srw-rw----   1 nobody    nobody     0 Mar 17 20:20 php-fpm.sock=
     drwxrwxr-x@  3 atinosun  staff     96 Jul 31  2018 webroot/
     ```

- 更改nginx配置

  - 将所有的配置文件中的fastcgi_pass参数更改

    ```bash
    fastcgi_pass  unix:/Users/atinosun/environment/php-fpm.sock;
    ```

  > 注意：nginx.conf中如果有默认的fastcgi_pass参数  给注释掉就好了
  >
  > 每个配置文件都需要写一遍，感觉好麻烦，找到可以全局用的方式再补充。

  - 重启nginx

    ```bash
    sudo nginx -s reload
    ```

- 此时已经可以看到本地的网站可以正常访问了



参考文章：

1. https://www.cnblogs.com/zzyyxxjc/p/4361282.html