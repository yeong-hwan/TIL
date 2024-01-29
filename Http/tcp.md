# TCP & UDP

### Date: 2024.01.30

---

### IP 스택의 4 계층
- 애플리케이션 계층: **HTTP, FTP**
- 전송 계층: **TCP, UDP**
- 인터넷 계층: **IP**
- 네트워크 인터페이스 계층

### 프로토콜 계층
![](img/tcp_1.png?raw=true)

### TCP/IP 패킷 정보
![](img/tcp_2.png?raw=true)

### TCP 특징
전송 제어 프로토콜(Transmission Control Protocol)
- 연결지향 - TCP 3 way handshake (가상 연결)
- 데이터 전달 보증
- 순서 보장
- 신뢰할 수 있는 프로토콜
- 현재는 대부분 TCP 사용 

### 3 Way Hanshake
![](img/tcp_3.png?raw=true)

### UDP 특징
사용자 데이터그램 프로토콜(User Datagram Protocol)
- 하얀 도화지에 비유(기능이 거의 없음)
- 연결지향 X - TCP 3 way handshake X
- 데이터 전달 보증 X
- 순서 보장 X
- 데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠름
- 정리
  - IP와 거의 같다. +PORT +체크섬 정도만 추가
  - 애플리케이션에서 추가 작업 필요