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
* 신뢰성있는 데이터 통신을 가능하게 해주는 프로토콜 (규약이므로)      
* 특징: Connection 연결 (3 way-handshake) - 양방향 통신/응답요청
* 데이터 순차 전송을 보장       
* Flow Control (흐름 제어)   
* Congestion Control (혼잡 제어)
* Error Detection (오류 감지)    

## 세그먼트 Segment - TCP 프로토콜의 PDU    


# 참고  
블로그   
https://securitycream.tistory.com/7 - Endpoint 용어    
   
