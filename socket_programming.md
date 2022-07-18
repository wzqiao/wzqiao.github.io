## htonl 函数
## socket
<p>socket 是计算机之间的进行通信的一种方式，通过socket这种约定，计算机之间可以互相通信<br></p>
<h3> UNIX/LINUX 中的socket</h3>
<p>Linux下 include<sys/socket>头文件来使用socket()函数来创建套接字
  <br>int socket(int af, int type, int protocol);
  <br>参数说明： int af 是地址族(Address family)，也就是ip地址的类型，常用的有AF_INET = PF_INET(ipv4) 和AF_INET6(ipv6). 
  <br>AF(Address family),PF(Protocol family).
  <br>本机地址 localhost = 127.0.0.1 
  <br>
  <br>int type 表示为数据传输方式/套接字类型。 常用的有 SOCK_STREAM（流格式套接字/面向连接的套接字）（TCP）和SOCK_DGRAM（数据报套接字/无连接的套接字）（UDP）
  <br>
  <br>int protocol 表示为传输协议 可以填0 只要前面两个参数写对了系统会自动判断类型, IPPROTO_TCP 和 IPPTOTO_UDP，分别表示 TCP 传输协议和 UDP 传输协议.
  <br>例子：
  <br>int tcp_socket = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);  //IPPROTO_TCP表示TCP协议
  <br>int udp_socket = socket(AF_INET, SOCK_DGRAM, IPPROTO_UDP);  //IPPROTO_UDP表示UDP协议
  <br>int tcp_socket = socket(AF_INET, SOCK_STREAM, 0);  //创建TCP套接字
  <br>int udp_socket = socket(AF_INET, SOCK_DGRAM, 0);  //创建UDP套接字
  <br>SOCK_STREAM 有以下几个特征：
    <ul>
      <li>数据在传输过程中不会消失；</li>
      <li>数据是按照顺序传输的；</li>
      <li>数据的发送和接收不是同步的（有的教程也称“不存在数据边界”）。</li>
  </ul>
    如果数据损坏或丢失，可以重新发送。
    可以将 SOCK_STREAM 比喻成一条传送带，只要传送带本身没有问题（不会断网），就能保证数据不丢失；同时，较晚传送的数据不会先到达，较早传送的数据不会晚到达，这就保证了数据是按照顺 
    序传递的。
  <br>
  <br>数据报格式套接字（Datagram Sockets）也叫“无连接的套接字”，在代码中使用 SOCK_DGRAM 表示。
      计算机只管传输数据，不作数据校验，如果数据在传输中损坏，或者没有到达另一台计算机，是没有办法补救的。也就是说，数据错了就错了，无法重传。
      因为数据报套接字所做的校验工作少，所以在传输效率方面比流格式套接字要高。
  <br>
    <ul>SOCK_DGRAM 有以下特征：
        <li>强调快速传输而非传输顺序；</li>
        <li>传输的数据可能丢失也可能损毁；</li>
        <li>限制每次传输的数据大小；</li>
        <li>数据的发送和接收是同步的（有的教程也称“存在数据边界”）。</li>
    </ul>
</p>
