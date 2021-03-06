---
layout: post
title: UDP中使用connect的作用
categories:
- NETWORK
---

udp协议提供的是面向非连接的服务，通信双方不需要建立连接。一方只需要建立好套接字，并显式或由系统绑定地址和端口号后就可以发送/接收数据包。

和tcp不同的是，使用udp协议的数据报套接字(SOCK_DGRAM)并不限定唯一的通信方。

既可以发送（sendto）数据给任意的接受方，也可以从任意的发送方接收（recvfrom）数据。

如果希望为一个数据报套接字指定唯一的通信方时，可以使用connect来实现这一功能。

需要注意的是，在数据报套接字上使用connect并**不是建立连接**，**不存在“握手”**的过程。**仅仅是为这个套接字指定一个通信方**，一旦指定了对方的地址，就可以通过send/recv来发送/接收数据了。

而且可以在这个数据报套接字上**多次调用connect函数来指定不同的通信方**。
