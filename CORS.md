# CORS
> Cross-Origin Resource Sharing   
> **교차 출처 자원 공유**      
          
# 출처    
![uri-structure](https://user-images.githubusercontent.com/50267433/99033470-4b2a2800-25be-11eb-99ed-3964a246ff2e.png)

|protocol|Host|Port|Path|QueryString|Fragment|
|--------|----------|-----|-------|---------------------|-----|
|https://|github.com|:433/|kwj1270|?q=김우재 &sort=oldset|#foo|

    
* 출처를 판단하는 기준으로 `Protocol-Host-Port` 가 같다면 같은 출처라고 말을한다.      
* 단, Port는 브라우저마다 정책이 다르다.(IE에서는 포트 포함 안함)      
   
**출처 확인 방법**
```javascript
console.log(location.origin);  
https://github.com <- 응답
```
      
# SOP란?    
> Same-Origin-Policy    
> **동일 출처 정책**      
      
웹은 오픈되어 있는 공간이다 보니까 좋은 리소스는 물론, 나쁜 리소스도 존재하여 이를 통한 공격을 받을 수 있다.    
그렇기 때문에 동일한 출처인 경우에만 리소스를 받을 수 있게 한 정책이다.       
수시적으로 브라우저를 사용할 때 `http | https` 통신을 하면 모두 이 정책을 받게된다.        

**하지만**   
웹에는 많은 정보가 존재하고, 하나의 홈페이지에서 전혀 다른 홈페이지의 정보를 이용하고 싶다.   
그렇기 때문에 이를 해결해주기 위한 예외 조항들이 생겼다.   

* CORS 정책을 지킨 요청   
* 실행 가능한 스크립트   
* 랜더될 이미지    
* 스타일 시트     
...등등     
     
## 같은 출처 VS 다른 출처   
|기준 URL : |`https://taggle.kr`|
|-----------|-------------------|


|URL|SOP|이유|
|-------|-------------|-------|
|https://taggle.kr/bookmark|O|Protocol-Host-Port 동일|
|http://taggle.kr| X |Protocol이 다르다.|
|https://taggle.kr:443/bookmark?page=1|O|RFC 표준상 http/https 에서 포트 번호는 생략 가능 -> 443이 맞으니 같은 출처|
|https://api.taggle.kr|X|Host가 다르다.|
|https://taggle.kr:8080|?|<- 포트가 다르다. (IE == O, 이외 브라우저 X)|

* 출처에 대한 RFC의 표준이 없어서 `프로토콜-호스트-포트`까지 동일 출처로 인정하는지는 **각각의 브라우저 구현 정책에 따라 다르다.**     
* 대부분의 브라우저에서는 `프로토콜-호스트-포트`까지 동일 출처로 인정해준다.      
* IE에서만은 `프로토콜-호스트`정책을 이용해서 특별하게 관리해줘야 한다. (차라리 사용 하지말자 ^^)      

![ie_is_trash](https://user-images.githubusercontent.com/50267433/99033468-482f3780-25be-11eb-8619-65a1d8aab570.jpg)    
  
# CORS & SOP가 나오게 된 이유        
* CSRF    
* XSS     
    
CORS와 SOP는 인터넷의 공개성으로 인해 생기는 보안 취약점들을 이용한 CSRF 와 XSS 같은 공격 수단을 방어하기 위한 정책이다.    
    
# 동일 출처 인식 방법은? 
![cors](https://user-images.githubusercontent.com/50267433/99033464-45ccdd80-25be-11eb-8fcb-046c533f1b2e.png)       
     
```
Origin == Access-Control-Allow-Origin
```
     
**정리**    
* Requset 요청에 `Origin 헤더` 존재      
* Response 응답에 `Access-Control-Allow-Origin 헤더` 존재      
* Request의 `Origin 헤더`와 Response의 `Access-Control-Allow-Origin 헤더`가 같으면 같은 출처라 인식         

# CORS 시나리오  
* Preflight Request   
* Simple Request   
* Credentialed Request      

## Preflight Request      
> 예비 요청       
   
![cors-preflight](https://user-images.githubusercontent.com/50267433/99033458-3fd6fc80-25be-11eb-869b-1278e7bf17f0.png)    

* 브라우저는 요청을 한번에 보내지 않고 예비 요청과 본 요청을 나누어서 서버로 전송합니다.    
* 자바스크립트 : `fetch()` 메서드 수행 -> url 요청      
* 브라우저 : 요청 헤더에 Origin이라는 필드에 `요청을 보내는 출처`를 함께 담아보냅니다.         
    * 기본적으로 웹 클라이언트 어플리케이션이 다른 출처의 리소스를 요청할 때는 HTTP 프로토콜을 사용하여 요청을 보냅니다.   
* 서버 : 요청에 대한 응답을 할 때     
응답 헤더의 `Access-Control-Allow-Origin`필드 값에 `서버의 리소스를 접근하는 것이 허용된 출처`를 넣어서 보냅니다.        
* 이후, 브라우저는 요청의 `Origin`과 응답의 `Access-Control-Allow-Origin`을 비교하여 이 응답이 유효한 응답인지 아닌지를 판단합니다.   
    * 유효한 응답 : 
    * 유효하지 않은응답 


 
# 결론 

# 참고 
블로그 :   
https://evan-moon.github.io/2020/05/21/about-cors/        
https://developer.mozilla.org/ko/docs/Web/HTTP/CORS   
https://developer.mozilla.org/ko/docs/Glossary/Preflight_request   

동영상 :   
