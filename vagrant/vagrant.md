#Vagrant使用教程

### 基础环境
- VirtualBox
  下载地址：https://www.virtualbox.org/wiki/Downloads
- Vagrant：
  下载地址：https://releases.hashicorp.com/vagrant/

### 启动虚拟机
- box下载
      http://www.vagrantbox.es/
```
    vagrant box add {title} {url}
    vagrant init {title}
    vagrant up
    vagrant ssh
```

### 虚拟机优化
- 修改阿里云源

  ```
  sudo mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
  wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
  yum clean all
  yum makecache
  ```

- 安装nginx
    + 阿里云yum源没有nginx。需要在添/etc/yum.repos.d/CentOS-Base.repo
    ```
    [nginx]
    name=nginx repo
    baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
    gpgcheck=0
    enabled=1
    ```

    + 开启nginx
    `systemctl start nginx`
    + 测试是否开启
    `curl -I 'http://127.0.0.1'`
    ```
    HTTP/1.1 200 OK
    Server: nginx/1.14.2
    Date: Mon, 25 Feb 2019 07:55:37 GMT
    Content-Type: text/html
    Content-Length: 612
    Last-Modified: Tue, 04 Dec 2018 15:03:06 GMT
    Connection: keep-alive
    ETag: "5c06972a-264"
    Accept-Ranges: bytes
    ```
- 安装msql碰到的问题
  https://www.cnblogs.com/starof/p/4680083.html

- 安装YII
  https://www.yiichina.com/doc/guide/2.0/start-installation
  
### 打包命令
`vagrant package --output xxx.box`

### 优化
-  虚拟机名称
    vb.name = "ubuntu_mooc"
- 虚拟机主机名
    config.vm.hostname = "mooc"
- 配置虚拟机内存和CPU
    vb.memory = "1024"
    vb.cpus = 2