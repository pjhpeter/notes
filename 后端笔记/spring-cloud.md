# 服务注册的坑
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