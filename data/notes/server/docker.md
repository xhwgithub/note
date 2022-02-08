# DOKCER

* 数据卷

> docker的镜像是由多个只读的文件系统叠加在一起形成的。当我们在我启动一个容器的时候，
> docker会加载这些只读层并在这些只读层的上面(栈顶)增加一个读写层。这时如果修改正在
> 运行的容器中已有的文件，那么这个文件将会从只读层复制到读写层。该文件的只读版本还在，
> 只是被上面读写层的该文件的副本隐藏。当删除docker,或者重新启动时，之前的更改将会消失。
> 在Docker中，只读层及在顶部的读写层的组合被称为Union File System（联合文件系统）

* docker 查看完整的执行语句  ___docker ps -a --no-trunc___

* 关键配置文件
  > /etc/docker/daemon.json
  ```
      {
      "api-cors-header":"",
      "authorization-plugins":[],
      "bip": "",
      "bridge":"",
      "cgroup-parent":"",
      "cluster-store":"",
      "cluster-store-opts":{},
      "cluster-advertise":"",
      "debug": true, #启用debug的模式，启用后，可以看到很多的启动信息。默认false
      "default-gateway":"",
      "default-gateway-v6":"",
      "default-runtime":"runc",
      "default-ulimits":{},
      "disable-legacy-registry":false,
      "dns": ["192.168.1.1"], # 设定容器DNS的地址，在容器的 /etc/resolv.conf文件中可查看。
      "dns-opts": [], # 容器 /etc/resolv.conf 文件，其他设置
      "dns-search": [], # 设定容器的搜索域，当设定搜索域为 .example.com 时，在搜索一个名为 host 的 主机时，DNS不仅搜索host，还会搜
      索host.example.com 。 注意：如果不设置， Docker 会默认用主机上的 /etc/resolv.conf 来配置容器。
      "exec-opts": [],
      "exec-root":"",
      "fixed-cidr":"",
      "fixed-cidr-v6":"",
      "graph":"/var/lib/docker", ＃已废弃，使用data-root代替,这个主要看docker的版本
      "data-root":"/var/lib/docker", ＃Docker运行时使用的根路径,根路径下的内容稍后介绍，默认/var/lib/docker
      "group": "", #Unix套接字的属组,仅指/var/run/docker.sock
      "hosts": [], #设置容器hosts
      "icc": false,
      "insecure-registries": [], #配置docker的私库地址
      "ip":"0.0.0.0",
      "iptables": false,
      "ipv6": false,
      "ip-forward": false, #默认true, 启用 net.ipv4.ip_forward ,进入容器后使用 sysctl -a | grepnet.ipv4.ip_forward 查看
      "ip-masq":false,
      "labels":["nodeName=node-121"], # docker主机的标签，很实用的功能,例如定义：–label nodeName=host-121
      "live-restore": true,
      "log-driver":"",
      "log-level":"",
      "log-opts": {},
      "max-concurrent-downloads":3,
      "max-concurrent-uploads":5,
      "mtu": 0,
      "oom-score-adjust":-500,
      "pidfile": "", #Docker守护进程的PID文件
      "raw-logs": false,
      "registry-mirrors":["xxxx"], #镜像加速的地址，增加后在 docker info中可查看。
      "runtimes": {
      "runc": {
      "path": "runc"
      },
      "custom": {
      "path":"/usr/local/bin/my-runc-replacement",
      "runtimeArgs": [
      "--debug"
      ]
      } },
      "selinux-enabled": false, #默认 false，启用selinux支持
      "storage-driver":"",
      "storage-opts": [],
      "swarm-default-advertise-addr":"",
      "tls": true, #默认 false, 启动TLS认证开关
      "tlscacert": "", #默认 ~/.docker/ca.pem，通过CA认证过的的certificate文件路径
      "tlscert": "", #默认 ~/.docker/cert.pem ，TLS的certificate文件路径
      "tlskey": "", #默认~/.docker/key.pem，TLS的key文件路径
      "tlsverify": true, #默认false，使用TLS并做后台进程与客户端通讯的验证
      "userland-proxy":false,
      "userns-remap":""
    }

  
   "insecure-registries": [],  #这个私库的服务地址

   "registry-mirrors": [],    #私库加速器
  ``` 

  > /etc/docker/key.json

* docker cp

  ```
  Docker cp # 从容器里面拷贝文件/目录到本地一个路径
  $docker cp Name:/container_path to_path  
  $docker cp ID:/container_path to_path//原文出自【易百教程】，商业转载请联系作者获得授权，非商业请保留原文链接：https://www.yiibai.com/docker/cp.html
  ```
* docker network
  ```
  docker network create my-net
  docker network rm my-net
   
  When you create a new container, you can specify one or more --network flags. This example connects a Nginx container to the my-net network. 
  It also publishes port 80 in the container to port 8080 on the Docker host, so external clients can access that port. 
  Any other container connected to the my-net network has access to all ports on the my-nginx container, and vice versa.
  
  docker create --name my-nginx --network my-net --publish 8080:80 nginx:latest
  ```