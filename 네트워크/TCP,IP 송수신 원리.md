# TCP/IP 송/수신 원리

- Socket 은 TCP/IP 를 추상화한 것이다.
- Socket 의 본질은 File 이다.

- Process 에서 File 을 RWX(read,write,execute) 하고,
- Socket 에서는 RW 를 하는데 Receive, Send 라고 부른다.


## 송신 측 
----
Process 에서 할당받은 Memory(Buffer) 에 쓴 파일을 TCP Buffer 로 Copy 하는 것을 Buffered I/O 라고 한다.
TCP 에서 이렇게 Copy 한 파일의 일부분을 Segment 로 IP 계층으로 보낸다. 
IP 계층에서는 이를 Packet 이라고 한다. (택배 박스)
NIC 계층에서는 Frame 이라고 한다. (트럭)
네트워크를 이동하는 동안 Frame 은 여러번 바뀔 수 있다.  
  
    
## 수신 측
----
TCP Buffer 에서 Process Buffer 로 데이터를 Copy 한다. 
이 속도는 네트워크 속도보다 빨라야한다.
TCP buffer 의 사이즈를 window size 라고 한다.  
  
## 수신 측 Buffered I/O 가 네트워크 속도보다 빨라야 하는 이유 
----
예를 들어 1~10까지의 Segment를 송신해야 할 때, 
이걸 한 번에 다 보내지 않고 1,2번 Segment 만 먼저 보내고 Wait 를 한다. => TCP 속도 지연의 이유 중 하나.

수신 측에서 받았다고 Ack 3을 보내면 송신이 3을 보내려고 하는데, 이 때.
수신 측의 Ack 에는 수신 Window Buffer 의 사이즈 정보도 포함되어 있다.
이 window buffer 의 사이즈가 Segment 3 의 MSS(Maximun Segment Size) 보다 작으면 송신 측은 보내지 않고 계속 Wait 를 한다.

그래서 파일 수신 속도가 느리다면 송신 측의 문제가 아니라 수신 측의 문제일 가능성도 있다.
그러므로 파일 검증 작업은 프로세스의 메모리로 먼저 올린다음 하는 것이 바람직하다.

  \
  ![default](/img/TCP.png)

