# Internet Protocol

### Date: 2024.01.28

---

### IP: Internet Protocol
![](img/internet_protocol_1.png?raw=true)

**IP의 역할**
- 지정한 IP 주소(IP Address)에 데이터 전달
  - 클라이언트인 내가 IP 주소를 부여받는다.
- **패킷(Packet)** 이라는 통신 단위로 데이터 전달

![](img/internet_protocol_2.png?raw=true)

- 패킷에 출발 IP, 목적 IP를 기재하고 내용물(Data)를 담는다.

![](img/internet_protocol_3.png?raw=true)
![](img/internet_protocol_4.png?raw=true)

- 정해진 규약(IP)에 의해 패킷이 목적지에 전달된다.
- 목적지에서 그에 대한 응답을 회신한다.

### IP 프로토콜의 한계
- 비연결성
  - 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송
- 비신뢰성
  - 중간에 패킷이 사라지면?(패킷 소실)
  - 패킷이 순서대로 안오면?(전달 순서 문제)
- 프로그램 구분
  - 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이면?

### Conclusion
IP 프로토콜 만으로는 문제를 해결할 수 없다!
-> 해결책이 바로 TCP 프로토콜