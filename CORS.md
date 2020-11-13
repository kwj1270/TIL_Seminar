# CORS
> Cross-Origin Resource Sharing   
> **교차 출처 자원 공유**      
          
# 출처    
`https://github.com:433/woowacourse/jwp-was/issues?q=럿고&sort=oldset#foo`
   
* Protocol : `https://`
* Host : `github.com`
* Port : `:433/`
* Path : `woowacourse/jwp-was/issues`
* QueryString : `?q=럿고&sort=oldset` 
* Fragment : `#foo`
    
출처를 판단하는 기준은 `Protocol-Host-Port` 가 같다면 같은 출처라고 가정한다.      
단, Port는 브라우저마다 정책이 다르다.(IE에서는 포트 포함 안함)      
   
**출처 확인 방법**
```javascript
console.log(location.origin);  
```
      
# SOP란?    
> Same-Origin-Policy    
> **동일 출처 정책**      
      
웹은 오픈되어 있는 공간이다 보니까 좋은 리소스는 물론, 나쁜 리소스도 존재하여 이를 통한 공격을 받을 수 있다.  
그렇기 때문에 동일한 출처인 경우에만 리소스를 받을 수 있게 한 정책이다.    
   
수시적으로 브라우저를 사용할 때 `http | https` 통신을 하면 모두 이 정책을 받게된다,   

**하지만**   
웹에는 많은 정보가 존재하고, 하나의 홈페이지에서 전혀 다른 홈페이지의 정보를 이용하고 싶다.   
그렇기 때문에 이를 해결해주기 위한 예외 조항들이 생겼다.   

* CORS 정책을 지킨 요청   
* 실행 가능한 스크립트   
* 랜더될 이미지    
* 스타일 시트     
...등등     
     
## 같은 출처 VS 다른 출처   
```
https://taggle.kr <- https 이므로 기본 포트가 443이다.  

https://taggle.kr/bookmark O  
http://taggle.kr X -> Protocol이 다르다.       
https://taggle.kr:443/bookmark?page=1 O -> RFC 표준상 http | https 에서 포트 번호는 생략가능하므로 443이 맞다면 같은 출처다.     
https://api.taggle.kr X -> Host가 다르다.      
https://taggle.kr:8080 X <- 포트가 다르다. (IE 에서는 O)     
```
* 출처에 대한 RFC의 정확한 표준이 없어서 `프로토콜-호스트-포트`까지 동일 출처로 인정하는지는 **각각의 브라우저 구현 정책에 따라 다르다.**     
* 대부분의 브라우저에서는 `프로토콜-호스트-포트`까지 동일 출처로 인정해준다.      
* IE에서만은 `프로토콜-호스트`정책을 이용해서 특별하게 관리해줘야 한다. (차라리 사용 하지말자 ^^)      
     
# CORS & SOP가 나오게 된 이유  
* CSRF    
* XSS     
    
CORS와 SOP는       
인터넷의 공개성으로 인해 생기는 보안 취약점들을 이용한 CSRF 와 XSS 같은 공격 수단을 방어하기 위한 정책이다.    
    
# 동일 출처 인식 방법은? 
```
Origin == Access-Control-Allow-Origin
```
* Requset 요청에 `Origin 헤더` 존재      
* Response 응답에 `Access-Control-Allow-Origin 헤더` 존재      
* Request의 `Origin 헤더`와 Response의 `Access-Control-Allow-Origin 헤더`가 같으면 같은 출처라 인식         
     
# CORS 시나리오  





# 결론 
# 참고 
