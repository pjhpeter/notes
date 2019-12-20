### 服务注册的坑
错误写法
```
eureka:
  instance:
    hostname: localhost
  client:
    register-with-eureka: false # 注册中心不需要注册成微服务
    fetch-registry: false # 注册中心不需要被发现
    service-url: # Eureka客户端与Eureka服务端的交互地址，集群版配置对方的地址，单机版配置自 己（如果不配置则默认本机8761端口）
      default-zone: http://${eureka.instance.hostname}:${server.port}/eureka/
```
正确写法
```
eureka:
  instance:
    hostname: localhost
  client:
    register-with-eureka: false # 注册中心不需要注册成微服务
    fetch-registry: false # 注册中心不需要被发现
    service-url: # Eureka客户端与Eureka服务端的交互地址，集群版配置对方的地址，单机版配置自 己（如果不配置则默认本机8761端口）
      defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/ # 这是个坑啊，写default-zone是不行的！
```
### docker启动微服务的坑
用docker启动微服务，eureka会把docker的虚拟ip注册进去，这样消费者可能会访问不了，所以创建容器的时候要加上--net=host这个参数，使用宿主机ip
```
docker run -id --name product_service -p 8001:8001 --net=host a22c5cac1c13
```