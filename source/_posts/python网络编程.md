---
title: python网络编程
date: 2020-07-08 11:46:04
tags: 网络编程 python
---
## 套接字类型
### 面向连接的套接字
    - 基于TCP/IP，使用SOCKET_STREAM作为套接字类型
### 无连接的套接字
    - 基于UDP/IP，使用SOCKET_DGRAM作为套接字类型

## pyhton中的网络编程
### socket模块
```python
socket(socket_family, socket_type, protocol = 0)
```
 - 其中socket_family 是选择网络类型,本地网（AF_UNIX）还是因特网(AF_INET)
 - socket_type 是选择套接字的类型, protocaol默认为0

 ### 套接字对象常用的方法
- 服务器套接字
```python 
s.bind() #将主机号端口号绑定到套接字上
s.listen() #设置并启动TCP监听器
s.accept() #被动接受客户端连接
```
- 客户端套接字
```python
s.connect() #主动发起TCP服务连接
s.connect_ex() #此时会以错误码的形式抛出问题而不是一大串异常
```
### 创建一个时间戳服务器
    