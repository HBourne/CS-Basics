## Network Interview Questions

#### 1. TCP三次握手
![](https://raw.githubusercontent.com/HIT-Alibaba/interview/master/img/tcp-connection-made-three-way-handshake.png)

#### 2. TCP四次挥手
![](https://raw.githubusercontent.com/HIT-Alibaba/interview/master/img/tcp-connection-closed-four-way-handshake.png)

#### 3. 浏览器从输入url到返还的过程


#### 4. TCP和UDP的区别
- TCP需要建立连接；UDP不需要
- TCP提供可靠服务，不丢失，内容无差错，不重复，按序到达；UDP尽最大努力交付，不保证可靠
- TCP有拥塞控制，UDP没有，更适合实时应用（视频会议等）
- TCP一对一；UDP可支持一对一，多对一，一对多
- TCP头部开销20字节；UDP头部开销8字节

#### 5. HTTPS原理，如何实现加密，客户端为何信任第三方证书


#### 6. TCP拥塞控制，如何避免拥塞
慢启动 - 指数增长发的包的数量，然后进入线性增长阶段直到达到阈值或者有丢失。发生拥塞后，将阈值降低，一般ssthresh的新的值为发生拥塞时的cwnd / 2。

#### 7. session，cookie和token


#### 8. 如何实现DNS劫持


#### 9. 如何控制客户端的并发数


#### 10. DNS的过程及实现方式


#### 11. HTTP和HTTPS区别


#### 12. 五层模型
- 应用层: HTTP, TFTP, FTP, SMTP, DNS
- 传输层: TCP, UDP
- 网络层: IP, ICMP, ARP, RARP, AKP, UUCP
- 数据链路层: Ethernet, PPP
- 物理层: IEEE 802.1A

#### 13. 七层模型
- 应用层: HTTP, FTP, SMTP, TFTP
- 表示层: Telnet
- 会话层: SMTP
- 传输层: TCP, UDP
- 网络层: IP, ICMP, ARP, RARP, AKP, UUCP
- 数据链路层: Ethernet, PPP
- 物理层: IEEE 802.1A

#### 14. TCP的时延体现在哪些方面？
TCP时延由延时确认机制导致。比如请求数据的时候，数据非常小，仅用10ms便发送完毕，但是建立连接花了30ms，那么总共花费了40ms才完成传输。

#### 15. Nagle算法
每次相应的数据包要凑够固定大小，Linux默认为1500字节

<!-- #### 16.  -->