# TCP UDP    
1. Transport Layer - 전송 계층     
2. TCP (Transfer Control Protocol)
3. UDP (User Datagram Protocol)   

# Transport Layer - 전송계층    
End Point간 **신뢰성**있는 데이터 **전송**을 담당하는 계층   
     
* 신뢰성 : 데이터를 `순차적`, `안정적인` 전달         
* 전송 : `포트 번호에 해당`하는 프로세스에 데이터를 전달      

즉, 신뢰성있는 데이터를 포트 번호에 해당하는 프로스세에 전달    

**EndPoint**
```
어떠한 소프트웨어나 제품에 최종목적지인 사용자를 가리키며 그 예로는 PC나 노트북, 핸드폰등 유저가 사용하는 devices등을 말함.
```

## Transport Layer -전송 계층 이 없다면    
* 데이터 순차 전송 원할히 X
  * 패킷의 순서가 뒤바껴져서 전송되어 수신자는 데이터를 해독할 수 없거나 추가 연산을 통해 처리해야한다.   
* Flow 흐름 문제   
  * 원인 : 송수신자 간의 데이터 처리 속도 차이가 처리할 수 있는 데이터량을 초과할 때 발생   
  * 데이터가 초과되면 누락되는 문제가 있다.   
* Congestion 혼잡 문제  
  * 원인 : 네트워크의 데이터 처리 속도(ex 라우터)가 혼잡할 때 발생      
  * 수신자에서 처리하는 속도가 느려진다.   
* 결과 : Hello nice to meet you -> Hell to you

# TCP (Transfer Control Protocol)   
**장점**   
* 신뢰성있는 데이터 통신을 가능하게 해주는 프로토콜 (규약이므로)      
* 특징: Connection 연결 (3 way-handshake) - 양방향 통신/응답요청
* 데이터 순차 전송을 보장       
* Flow Control (흐름 제어)   
* Congestion Control (혼잡 제어)
* Error Detection (오류 감지)    

**문제점**
* 매번 Connection을 연결해서 시간 손실 발생 (3-way handshake)
* 패킷을 조금만 손실해도 재전송     

## 세그먼트 Segment - TCP 프로토콜의 PDU    
[사진]    

### TCP Header    
[사진]    

## TCP의 3-way handshake (Connection 연결)    
    
![99087C405C18E3CD28](https://user-images.githubusercontent.com/50267433/99354570-07029480-28ea-11eb-9e82-4e9204a15663.png)    

```
1. 너 내 말 들리니 syn   
2. 응 들려 ack 너도 내말 들리니 syn   
3. 응 들려 ack      
```
* 클라이언트 -> 서버 : 연결 요청 패킷 SYN(a) 전송
* 서버 -> 클라이언트 : SYN(a) 받고, 연결 요청 응답 패킷 ACK(a+1)와 SYN(b) 연결 요청 패킷 전송
* 클라이언트 -> 서버 : ACK(a+1)와 SYN(b) 받고, 연결 요청 응답 패킷 ACK(b+1) 을 전속하면 연결이 성립됩니다.

## TCP 4-way Handshake     
  
![tcp4wayhandshake](https://user-images.githubusercontent.com/50267433/99354932-b8092f00-28ea-11eb-814a-1d1264486a9d.png)

* 클라이언트 -> 서버 : 연결 종료를 의미하는 FIN 플래그 전송
* 서버 -> 클라이언트 : FIN 플래그 받고 확인 패킷 ACK 전송
* 그리고 데이터를 모두 보낼때까지 잠깐 TIME_OUT
* 서버 -> 클라이언트 : 데이터 모두 보내고 통신이 끝났으면 연결 종료 FIN 플래그 전송
* 클라이언트 -> 서버 : FIN 메시지 확인후 확인 패킷 ACK 전송
* 서버 : 클라이언트의 ACK를 받으면 소켓 연결 CLOSE
* 클라이언트 : 서버로부터 아직 받지 못한 데이터 대비해 일정시간 동안 대기 TIME_OUT

# UDP (User Datagram Protocol)   
* TCP보다 신뢰성이 떨어지지만 전송 속도가 일반적으로 빠른 프로토콜       
     * 순차 전송 X
     * 흐름 제어 X
     * 혼잡 제어 X
* Connectionless (3 way-handshake X)     
     * 단방향  
* Error Detection   
* 비교적 데이터의 신뢰성이 중요하지 않을 때 사용(ex 영상 스트리밍)        
  
## User Datagram - UDP 프로토콜의 PDU  
  
[사진]   

## UDP의 데이터 전송 방식

# 중요한 점   
* TCP, UDP의 특성을 파악하고 상황에 따라 적절한 프로토콜을 사용할 수 있다.   
* TCP, UDP의 헤더에 대해 파악하고 성능 개선에 이용할 수 있다.   


# 참고  
블로그   
https://securitycream.tistory.com/7 - Endpoint 용어    
   
