## Network Interview Questions

#### 1. TCP三次握手
![](https://raw.githubusercontent.com/HIT-Alibaba/interview/master/img/tcp-connection-made-three-way-handshake.png)

#### 2. TCP四次挥手
![](https://raw.githubusercontent.com/HIT-Alibaba/interview/master/img/tcp-connection-closed-four-way-handshake.png)

#### 3. 浏览器从输入url到返还的过程
- DHCP配置主机信息
- ARP解析路由器MAC地址
- 转发DNS报文至DNS server
- 建立TCP连接
- 发送HTTP请求
- 服务器处理请求并返回HTTP报文
- 浏览器渲染内容
- 结束连接

#### 4. TCP和UDP的区别
- TCP需要建立连接；UDP不需要
- TCP提供可靠服务，不丢失，内容无差错，不重复，按序到达；UDP尽最大努力交付，不保证可靠
- TCP有拥塞控制，UDP没有，更适合实时应用（视频会议等）
- TCP一对一；UDP可支持一对一，多对一，一对多
- TCP头部开销20字节；UDP头部开销8字节

#### 5. HTTPS原理，如何实现加密，客户端为何信任第三方证书
1. 客户端使用https的url访问服务器，要求与服务器建立ssl连接
2. 服务器收到请求后，会将网站的证书信息（包含公钥）发给客户端
3. 客户端的浏览器与服务器开始协商ssl连接的安全等级
4. 客户端的浏览器根据安全等级简历会话密钥，利用网站的公钥将会话密钥加密，并传给server
5. 服务器用私钥解密出会话密钥
6. 客户端和服务器使用会话密钥加密通信

伪造证书基本不可能，且申请有效证书的门槛非常高，且基本强制安装在浏览器内

#### 6. TCP拥塞控制，如何避免拥塞
慢启动 - 指数增长发的包的数量，然后进入线性增长阶段直到达到阈值或者有丢失。发生拥塞后，将阈值降低，一般ssthresh的新的值为发生拥塞时的cwnd / 2。

#### 7. session，cookie和token
Session：用于标记跟踪用户。

Cookie：实现验证用户信息，包含session id以及其他credential信息用于验证。服务器需要存储session等相关信息以便验证。用户登录后需服务器和客户端同时销毁会话。服务器验证会话id以决定是否继续处理相关请求。

Token：验证是无状态的，对服务器的每个请求都会带上token，可以加在header中也可以放在post之类的body里，在用户退出登录后销毁token。服务器不需要存储token只需要验证，并负责给成功登陆的请求签署token。

#### 8. 如何实现DNS劫持
获取路由器登录权限后，通过篡改dns服务器ip列表的方式进行dns劫持。通过检查以上配置，可以进行防范，做好设备的漏洞修复以及修改密码等。

#### 9. 如何控制客户端的并发数
通过修改nginx.conf里的http{}相关配置

#### 10. DNS的过程及实现方式
- 用户运行dns客户端
- 浏览器从接收到的url中提取域名，并将这个主机名发送给dns应用的客户端
- dns客户端向dns服务器发送查询报文
- dns客户端收到回应，包含该主机名对应的ip地址

#### 11. HTTP和HTTPS区别
- https需要到ca申请证书，一般免费证书较少，需要付费
- http是超文本传输协议，信息明文传输，https则通过ssl加密传输协议
- 连接方式以及端口不同，前者80，后者443
- http无状态，https是由ssl+http构建的可加密、身份认证的网络协议，比http更加安全

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

#### 16. HTTP/1.x和HTTP/2.0
- HTTP/1.x缺点
    - 需要多个TCP连接实现并发和缩短延迟
    - 不压缩请求和响应头部
    - 不支持有效的资源优先级，使底层TCP连接的利用率低下
- HTTP/2.0
    - 将报文分成HEADERS和DATA
    - 只有一个TCP连接，承载了任意数量的双向数据流
    - 每个stream都有一个唯一标识符和可选的优先级信息
    - 帧(frame)是最小通信单位
    - 在客户端请求资源时，会把相关资源一起发给客户端
    - 要求Server与Client同时维护首部字段表，避免重复传输

<!-- #### 17.  -->