# OSI_7_Layer.md 
# Physical Layer    
## 컴퓨터의 통신   
모든 파일과 프로그램은 사실 `0`과 `1`의 나열이다.           
그렇기에 컴퓨터간에 데이터를 통신하는 것은 `0`과 `1`을 교류하는 것이다.            

**그렇다면 `0`과 `1`을 어떻게 구분해서 통신을 할까? 🤔**   

* 1 : `+5v`의 전기적 신호  
* 0 : `-5v`의 전기적 신호 

위 2가지 방식을 통해서 우리는 `1`과 `0`의 전기적 신호를 보낼 수 있고  
이를 이용하여 다른 컴퓨터에 데이터를 보내는 `통신`이 가능하다.       

하지만 이 간단한 아이디어는, 실생활에는 적용하기 어려운 문제가 많았다.      
**그 이유는 무엇일까? 🤔**  

[사진]()   
  
위 그림은 전자기파(아날로그 신호)를 표현한 함수이다.      
가로로는 시간, 세로로는 전압의 크기를 나타내고 있다.        
       
전자기파에서 1초 동안의 사이클 횟수를 우리는 주파수/헤르츠(Hz) 라고 부른다.    
    
[사진]()      
     
하지만, 전자기파는 주파수 값이 숫자 하나로 고정되지는 않는다.       
위 그림의 전자기파는 파동이 진행되는 동안 주파수 값이 계속 변한다.    
(여기서 말한 전자기파는 아날로그 신호라고 보면 됩니다.)   
   
**예시**   
위 그림의 전자기파수의 범위는 아래와 같다고 가정한다.   
   
* 최소 주파수(hz)값은 1,     
* 최대 주파수(hz)값은 10    

**전선은 모든 주파수를 통과하지 못한다. (사실, 모든 매질들이 그렇다)**        
어떤 전선이 `5hz` ~ `8hz`의 전자기파만 통과시킨다고 가정하자   
        
그렇다면, `1~4hz`와 `9~10hz`는 통과하지 못하게 되며     
최종적으로는 `5hz` ~ `8hz`와 손실된 `1~4hz 및 9~10hz`가 전송되게 된다.      
    
2대의 검퓨터가 통신하려면 0과 1의 신호만을 주고 받을 수 있으면 된다.      
즉, 2대의 컴퓨터가 위 그림과 같은 전자기파만 보낼 수있으면 된다.    
(컴퓨터는 디지털 신호만 보낸다.)    
   
그런데, 수직선과 수평선이 있는 전자기파는 항상 `0hz` ~ `무한hz`의 주파수 범위를 가진다.   
따라서 위와 같은 전기신호를 통과시킬 수 있는 전선은 없다.    

**그렇다면 이 신호를 어떻게 전송해야 할까? 🤔**   

[사진]()   

위 그림처럼 디지털 신호를 아날로그 신호로 바꿔서 동작시켜야한다.    
즉, 데이터를 송신하는 컴퓨터는 `디지털 신호`를 `아날로그 신호`로 `encoding`하여 전선에 보내고  
데이터를 수신하는 컴퓨터는 전선으로부터 전송되어진 `아날로그 신호`를 `디지털 신호`로 `decoding`하여 해석한다.   
       
## 그래서 결국 Physical Layer 란        
`0`과 `1`의 나열을 아날로그 신호로 바꾸어 전선으로 흘려보내고 (encoding)        
아날로그 신호가 들어오면 이를 `0`과 `1`의 나열로 해석한다. (decoding)        
결론적으로 물리적으로 연결된 2대의 컴퓨터가 `0`과 `1`의 나열을 주고받을 수 있게 해주는 모듈이다.       

모듈이란건, 설명하기 어렵지만 함수와 비슷하다고 생각하면 된다.    

[사진]()  
  
이러한 `Physical Layer` 기술은   
`PHY`라는 칩에 구현되어 있다.   
그리고 1계층 모듈은 하드웨어적으로 구현되어 있다.(회로)   
사실, 하드웨어도 Input 을 받아서 Output을 만들어내기에 함수로 비유를 했다.    
  
# Data-Link Layer     
## 여러대의 컴퓨터 간의 통신       
두 대의 컴퓨터는 서로간에만 전선을 연결하면 된다.      
**그렇다면 여러 대의 컴퓨터가 있다면 이들 각가마다 전선을 연결해야 할까? 🤔**      

[사진]()   

이러한 방식으로 전선을 연결한다면 데이터 전송 측면에서 매우 효율적이겠지만,        
사실 비용이 많이들고 각각의 전선을 연결하는 단자, 비용도 많이 들 것이다.      
따라서, **전선 하나를 가지고 여러 대의 컴퓨터와 통신할 방법을 모색하기 시작했다.**      

## 버스(Bus)   
     
[]()   
    
위와 같이 하나의 전선에 여러 대의 컴퓨터가 연결된 구조를 `버스(bus)`라고 부른다.      
`버스`를 통해, 단 하나의 회선으로 여러 컴퓨터들간에 통신을 할 수 있게 되었다.   
     
하지만, 여기에는 몇가지 문제점이 있다.         
**전기가 통하는 구리선**에 여러 대의 컴퓨터가 연결되었다고 가정을 한다.       
만약, 한 컴퓨터가 다른 특정 컴퓨터에게 `0010 0100`과 같은 데이터를 보내기 위해서 구리선으로 신호를 보낸다면             
구리선은 전기가 통하므로, **신호는 구리선의 모든곳으로 전달되어서 모든 컴퓨터로 전달된다.**          
즉, 버스를 통해 특정 컴퓨터에게 데이터를 보내는 것은 성공했지만,         
이와 상관없는 **다른 컴퓨터에서도 해당 데이터를 수신한다는 문제가 있다.**        

## 더미허브와 스위치 

[사진]()   


`버스(bus)` 구조를 위 그림과 같은 형태를 만들었다고 가정하자          
그리고, 위 그림에서 네모칸은 **[더미허브]()** 를 뜻한다.        
      
`더미허브`는 허브에 연결된 컴퓨터들에게 네트워크상의 데이터를 전달하는 기능만 한다.        
그렇기 때문에, 버스(bus)에서 발생하는 문제점들인 다른 컴퓨터에게도 데이터를 보내는 문제를 해결해줄 수 없다.        
             
그런데 만약, 이 허브가 **메시지의 목적지를 확인해서 특정 컴퓨터에게만 데이터를 전달해줄 수 있으면 어떨까? 🤔**       
이러한 생각에서 고안된 것이 바로, **스위치**이다.      
**`스위치`는 메시지의 목적지를 확인해서 특정 컴퓨터에게만 데이터를 전달해줄 수 있다.**            
(스위치는 일종의 컴퓨터로서 이러한 일들을 수행한다.)     
       
스위치로 연결된 컴퓨터들간의 구조를 우리는 `네트워크`라고 부른다.   
또한, 단순히 스위치로만 연결된 컴퓨터들간의 구조를 `인트라넷`이라고도 부른다.   
   
## 라우터       
**서로 다른 네트워크(인트라넷)에 있는 컴퓨터에 데이터를 보내려면 어떻게 해야할까? 🤔**     
   
당연하게도 서로 다른 두 개의 컴퓨터는 전선으로 연결되어 있지 않으면 통신을 할 수 없다.       
그렇기에 **서로 다른 네트워크끼리 통신을 하려면 `스위치`와 `스위치`를 연결해주면 된다.**        
그리고 이와 같이 서로 다른 네트워크에 속한 컴퓨티끼리 통신이 가능하게 해주는 장비를 **라우터**라고 한다.   
  
엄밀히 말하자면, `라우터 + 스위치`기능을 가진 `L3 스위치`이다.        
이해를 돕기위해 우리의 실생활에서 찾아볼 수 있는 물건으로 `공유기`가 있다.    

**이제, 더 많은 네트워크끼리 연결하려면 어떻게 해야할까? 🤔**   

[사진]() 
  
`라우터`는 `이미 한번 라우터로 이루어진 네트워크`와도 연결이 가능하다.      
이들을 쭉 엮다보면 거대한 네트워크가 형성될 것 이고 이를 우리는 `인터넷`이라고 부른다.      
     
네트워크 범위를 식별하다보면, 각 나라별로 존재하는 것을 알 수 있다.      
각 나라별 거리는 엄청나게 길기에 각 나라의 네트워크를 연결하는 전선은 아주 길다.(해저케이블)      

## Data-Link Layer    
`Data-Link Layer` 는 여러대의 컴퓨터 통신과 밀접하게 연결되어 있다.   
예를 들어 현재 네트워크나, 전세계 네트워크에서 나에게 다량의 데이터를 보낸다고 가정한다.   
     
* 1번 컴퓨터 : 0101   
* 2번 컴퓨터 : 1111    
* 3번 컴퓨터 : 0001    
    
만약, 데이터를 수신 받는 컴퓨터에서 각 컴퓨터별로 보낸 데이터를 구분할 수 없다면?        
`010111110001` 과 같은 식별을 할 수 없는 데이터가 될 것이다.      
     
**그렇다면, 어떻게 끊어 읽어야 할까? 🤔**       
각각의 컴퓨터마다 보내준 데이터를 구분 하기 위해서        
**송신자(송신 컴퓨터)는 데이터의 앞 뒤에 특정한 비트열을 붙여서 보내도록 규정했다.**       
         
예를들어, 송신자(송신 컴퓨터)가 데이터를 보낼때 앞에는 1111, 뒤에는 0000을 붙인다 가정하다.        
수신자가 `0000 1111 0110 1000 0001 1111 1011 0000 1111`과 같은 데이터를 받았다면은      
0000 `1111` 0110 100`0 000``1 111`1 1011 `0000` 1111 과 같이 구분을 할 수 있게 된다.       

## 그래서 결국 Data-Link Layer란,   
* 같은 네트워크에 있는 여러 대의 컴퓨터들이 데이터를 주고받기 위해서 필요한 모듈   
* `Framing`은 `Data-lnik Layer`에 속하는 작업들 중 하나이다.    

**인코딩 디코딩 흐름**     
   
[그림]()    

**송신 컴퓨터**
2. 2계층은 `Framing`을 통해 데이터를 구분하기 위한 구분 비트를 추가한다.    
3. 1계층은 디지털 신호를 아날로그 신호로 바꾸어 전선에 흘려보낸다.   
  
**수신 컴퓨터/각각의 라우터**     
1. 1계층은 아날로그 신호를 디지털 신호로 바꾸어 2계층에 올린다.     
2. 2계층은 받은 데이터에서 구분 비트를 기준으로 변경한다.      
     
이러한 `Data-Link Layer` 기술은 `랜카드`에 구현되어 있다.   

# Network Layer   
   
[사진]()   
        
위 그림에서 A라는 컴퓨터에서 B 라는 컴퓨터로 데이터륿 보내고 싶어한다.        
사실 앞서 설명은 안했지만, `스위치`는 데이터의 목적지를 식별하는 기능을 가지고 있다고 했다.      
그렇다면 **`데이터의 목적지`를 식별할 수 있는 방법은 무엇일까? 🤔**      
    
이는 아마 대부분의 사람들이 알고 있을텐데 바로, **IP**이다.        
IP란, **각 컴퓨터들이 갖는 고유한 주소**를 의미한다.       
(고유한 식별자로 컴퓨터의 주민등록번호인 mac address 도 있는데, [ip 사용 이유](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=salc24&logNo=10067461377)에 대해서는 링크를 참조하자)       
   
그렇다면 `목적지의 IP주소를 어떻게 알지? 🤔`라는 의문점이 생긴다.      
우리는 IP 주소의 외우기 어려운 단점, IP 주소를 간편하게 찾기 위해 `Domain Name`을 사용한다.    

`Domain Name`이란, `IP`주소를 인간이 알아 볼 수 있도록 변환한 것이며   
`url`에 우리가 `Domain Name`을 입력하면 `DNS(Domain Name Server)`를 통해 실제 `IP` 주소로 처리된다.        
      
`ip주소 + 구분 비트 + 실제 데이터`를 우리는 **패킷**이라고 부를 수 있다.   
(원래 패킷은 데이터 원본을 전송을 위해 작게 자른 단위이다.)     
   
**통신 흐름**   
   
[사진]()    

A라는 컴퓨터에서 B라는 컴퓨터로 데이터를 보내는 과정을 해석하면 아래와 같다.   

1. 라우터가 패킷을 확인하여 현재 네트워크에 목적지가 있는지 확인한다.   
    * 패킷을 확인한다는 것은 `IP`와 관련된 부분을 분리하여 목적지를 확인한다.   
    * 그리고 다시 전송을 보낼때는 `IP`와 관련된 부분을 다시 결합하여 목적지로 보낸다.      
2. 존재하지 않는다면 상위 라우터로 패킷을 보낸다.    
3. 상위 라우터는 패킷을 받고 이제 어느 라우터로 데이터를 보낼지 계산을 한다.   
    * [라우팅 테이블](https://ko.wikipedia.org/wiki/%EB%9D%BC%EC%9A%B0%ED%8C%85_%ED%85%8C%EC%9D%B4%EB%B8%94)이라는 개념을 이용한다.       
4. 그리고 1-3번을 반복한다.   
5. 현재 네트워크에 목적지가 있는 것을 식별했다면 해당 컴퓨터에 패킷을 넘겨준다.   
    
## 그래서 결국 Network Layer란?      
수많은 네트워크들의 연결로 이루어지는 `inter-network`속에서      
어딘가에 있는 목적지 컴퓨터로 데이터를 전송하기 위해서 `IP 주소`를 이용해서 길을 찾고(routing)         
자신 다음의 라우터에게 데이터를 넘겨주는 것이다.(forwarding)       

**송신 컴퓨터**
1. 3계층은 목적지 식별을 위해 `IP`주소를 추가한다.  
2. 2계층은 `Framing`을 통해 데이터를 구분하기 위한 구분 비트를 추가한다.    
3. 1계층은 디지털 신호를 아날로그 신호로 바꾸어 전선에 흘려보낸다.   
  
**수신 컴퓨터/각각의 라우터**     
1. 1계층은 아날로그 신호를 디지털 신호로 바꾸어 2계층에 올린다.     
2. 2계층은 받은 데이터에서 구분 비트를 기준으로 변경한다.      
3. 3계층은 `IP` 주소를 제거한다.     
     
# Transport Layer     
위 `1~3 단계`를 통해서도 이제 전세계의 모든 컴퓨터와 통신을 할 수 있게 되었다.        
하지만, 이는 단 한개의 프로그램만 실행되었다고 가정을 하는 것이고       
사실 우리가 실행하고 있는 컴퓨터는 여러 프로그램을 실행하고 있다.        
      
**여러 프로그램을 실행하는 것과 무슨 상관이 있냐고 말할 수 있지만 사실 상관이 크다. 🤔**    
`IP`로만 통신을 한다고 가정하면, 받은 데이터를 어떤 프로그램(프로세스)에 나눠줘야할지 모르기 때문이다.    
      
이를 해결하기 위해서는 **데이터를 받고자 하는 프로세스들은 포트 번호라는 것을 가져야한다.**           
그리고 송신자는 데이터를 보낼 때, **데이터를 받을 수신자 컴퓨터에 있는 프로세스의 포트번호를 붙여서 보내야한다.**           
참고로, 포트 번호는 **하나의 컴퓨터에서 동시에 실행되고 있는 프로세스들이 서로 겹치지 않게 가져야하는 정수값이다.**       
     
**참고로**    
url의 `http`와 `https`의 포트번호는 생략 가능하다.        

**송신 컴퓨터**
1. 4계층은 데이터를 받을 프로세스의 포트 번호를 추가한다.   
2. 3계층은 목적지 식별을 위해 `IP`주소를 추가한다.  
3. 2계층은 `Framing`을 통해 데이터를 구분하기 위한 구분 비트를 추가한다.    
4. 1계층은 디지털 신호를 아날로그 신호로 바꾸어 전선에 흘려보낸다.   
  
**수신 컴퓨터/각각의 라우터**     
1. 1계층은 아날로그 신호를 디지털 신호로 바꾸어 2계층에 올린다.     
2. 2계층은 받은 데이터에서 구분 비트를 기준으로 변경한다.      
3. 3계층은 `IP` 주소를 제거한다.     
4. 4계층은 포트 번호를 통해 알맞는 프로세스에 데이터를 전달한다.   
     
`transport layer` 기술은 `운영체제의 커널`에 소프트웨어적으로 구현되어 있다.      
   
# Application Layer  
`OSI 7 Layer` 는 7계층으로 이루어져 있다.   
그런데 `Application Layer`는 7계층에 속해있다.   
그렇다면 중간에 있는 `Presentation Layer(6계층)` 와 `Session Layer(5계층)`를 생략하고   
왜 7계층인, `Application Layer`로 넘어왔지?   
    
사실 현대의 인터넷은 `OSI 모델`이 아니라 `TCP/IP 모델`을 따르고 있다.          
`TCP/IP 모델`도 `OSI 모델`과 마찬가지로 네트워크 시스템에 대한 모델이다.       
   
현대의 인터넷이 `TCP/IP` 모델을 따르는 이유는      
`OSI 모델` 보다 `TCP/IP 모델`이 시장 점유가 더 많기 때문이다.      
   
**TCP/IP**  
    
[사진]()   
    
`TCP/IP`는 `OSI 7 Layer`와 비슷한 구조를 가지며      
특정 레이어들은 하나로 뭉쳐져서 표현이 되는 것을 알 수 있다.       
    
그리고 더 진화되어 현재는 `TCP/IP Update` 라는 모델을 사용하고 있는데      
`1~4 계층`은 `OSI 7 Layer`와 동일한 모습인 것을 알 수 있다.       
그렇기 때문에 사실, 현재 더 많이 사용되는 `TCP/IP Update`모델로서 Application을 설명하고자한다.      
그리고 [정리를 아주 잘 해주신 사이트](https://velog.io/@amuse/OSI-7-Layers) 가 있어서 링크를 남긴다.   

**TCP/IP 소켓 프로그래밍**
* 운영 체제의 `Transport Layer` 에서 제공하는 `API`를 이용하여     
  통신 가능한 프로그램을 만드는 것을 `TCP/IP 소켓 프로그래밍`, 또는 `네트워크 프로그래밍`이라고 한다.      
* 소켓 프로그래밍만으로도 클라이언트, 서버 프로그램을 따라따로 만들어서 동작시킬 수 있다.   
  뿐만 아니라, `TCP/IP` 소켓 프로그래밍을 통해서 누구나 자신만의 `Application Layer` 인코더와 디코더를 만들 수 있다.      
  즉, 누구든 자신만의 `Application Layer` 프로토콜을 만들어서 사용할 수 있다는 뜻이다.   

`Application Layer` 도 다른 Layer 들과 마찬가지로 인코더, 디코더가 존재한다.   
대표적인 `Application Layer` 프로토콜로는 HTTP 인코딩 & 디코딩이 존재한다.   

**서버 컴퓨터**
1. 5계층은 `StatusCode`와 같은 http 요소를 데이터에 추가한다.   
1. 4계층은 데이터를 받을 프로세스의 포트 번호를 추가한다.   
2. 3계층은 목적지 식별을 위해 `IP`주소를 추가한다.  
3. 2계층은 `Framing`을 통해 데이터를 구분하기 위한 구분 비트를 추가한다.    
4. 1계층은 디지털 신호를 아날로그 신호로 바꾸어 전선에 흘려보낸다.   
  
**클라이언트 컴퓨터**     
1. 1계층은 아날로그 신호를 디지털 신호로 바꾸어 2계층에 올린다.     
2. 2계층은 받은 데이터에서 구분 비트를 기준으로 변경한다.      
3. 3계층은 `IP` 주소를 제거한다.     
4. 4계층은 포트 번호를 통해 알맞는 프로세스에 데이터를 전달한다.   
5. 5계층은 `StatusCode`와 같은 http 요소를 분리하여 상태를 확인하고 데이터를 얻는다.     







   

  

   












   










