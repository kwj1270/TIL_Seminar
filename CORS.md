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

* OPTIONS 메서드로 예비 요청을 보내고 본 요청을 보낸다.    
* Origin에 대한 정보 뿐만 아니라 자신이 예비 요청 이후 보낼 본 요청에 대한 다른 정보들도 같이 포함되어 있다.   
  * 예를 들어 Access-Control-Request-Headers, Access-Control-Request-Method 등)        
* 요청에 Origin 과 응답의 Access-Control-Allow-Origin 를 브라우저가 비교해 출처를 판단
  * 다름 : 에러를 발생 
  * 접근 가능 : 본 요청을 보내 요청을 처리   
* **서버 사이드 영역이 아닌 브라우저 영역이기 때문에 서버는 200대의 성공 코드를 반환한다.**        
  * 서버로부터 응답을 받은 후, 브라우저에서 동일 출처인지 비교하는 것     
  * CORS 정책 위반으로 인한 에러는 예비 요청의 성공 여부와 별 상관이 없다      
       
### 코드로 살펴보기 
* 환경 : 크롬 시작페이지에서 실행
* F12 키를 눌러 console 에서 진행   
   
**Request 보내기**
```javascript
const headers = new Headers({'Content-Type':'text/html',});
fetch('https://rutgo-letsgo.tistory.com/rss', {headers});
```

**Request 헤더**
```javascript
OPTIONS /rss HTTP/1.1
Host: rutgo-letsgo.tistory.com
Connection: keep-alive
Accept: */*
Access-Control-Request-Method: GET
Access-Control-Request-Headers: content-type
Origin: chrome://new-tab-page 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.198 Safari/537.36
Sec-Fetch-Mode: cors
Sec-Fetch-Site: cross-site
Sec-Fetch-Dest: empty
Accept-Encoding: gzip, deflate, br
Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
```

**Response 헤더**
```javascript
Access-Control-Allow-Origin: http://rutgo-letsgo.tistory.com
Content-Encoding: gzip
Content-Type: text/xml; charset=utf-8
Date: Fri, 13 Nov 2020 06:43:49 GMT
P3P: CP='ALL DSP COR MON LAW OUR LEG DEL'
Transfer-Encoding: chunked
Vary: Accept-Encoding
X-UA-Compatible: IE=Edge
```

**비교**
```javascript 
Request   | Origin: chrome://new-tab-page 
Response  | Access-Control-Allow-Origin: http://rutgo-letsgo.tistory.com
```

**결과 - ERROR**
```javascript
Access to fetch at 'https://rutgo-letsgo.tistory.com/rss' 
from origin 'chrome://new-tab-page' has been blocked by CORS policy: 
Response to preflight request doesn't pass access control check: 
The 'Access-Control-Allow-Origin' header has a value 'http://rutgo-letsgo.tistory.com' that is not equal to the supplied origin. 
Have the server send the header with a valid value, or, if an opaque response serves your needs, 
set the request's mode to 'no-cors' to fetch the resource with CORS disabled.
```

## Simple Request
> 단순 요청   
        
![simple-request](https://user-images.githubusercontent.com/50267433/99038351-af51e980-25c8-11eb-8c59-e747f00ffdca.png)      
    
* 요청의 메서드는 `GET, HEAD, POST` 중 하나여야 한다.  
  * `DELETE` 를 제외하고는 가능      
* `Accept, Accept-Language, Content-Language, Content-Type, DPR, Downlink, Save-Data, Viewport-Width, Width`   
를 제외한 헤더를 사용하면 안된다.
  * `Authorization`과 같은 JWT의 헤더를 사용할 수 없어 REST API 에서는 사용하기 힘들다.         
* 만약 `Content-Type`를 사용하는 경우에는 `application/x-www-form-urlencoded, multipart/form-data, text/plain`만 허용된다
   * `text/xml` 이나 `application/json` 를 사용할 수 없어 REST API에서는 사용하기 힘들다.  
  
가장 간단한 방법이지만 까다로운 제약사항으로 우리가 실제로 사용하기는 힘듭니다.    

## Credentialed Request
> 자격이 증명된 요청   
      
![with-credentials](https://user-images.githubusercontent.com/50267433/99038319-9f3a0a00-25c8-11eb-9b38-e536174ba921.png)
    
|옵션 값|설명|
|-------|---|
|same-origin (기본값)|같은 출처 간 요청에만 인증 정보를 담을 수 있다|	
|include|모든 요청에 인증 정보를 담을 수 있다|
|omit|모든 요청에 인증 정보를 담지 않는다|

* fetch() 나 비동기 API들은 일반적으로 Cookie를 담아서 보내지 않습니다.   
  * `fetch(credentialed : include)`
* Cookie를 담을 수 있는 옵션을 주어 서버에서 인증이 된 사용자인지 한번 더 검증을 거치는 작업이다.   
   
### 코드로 살펴보기 
* 환경 : 크롬 시작페이지에서 실행
* F12 키를 눌러 console 에서 진행   
   
**Request 보내기**
```javascript
fetch('https://rutgo-letsgo.tistory.com/rss', {credentials: "include"});
```

**Request 헤더**
```javascript
Accept: */*
Accept-Encoding: gzip, deflate, br
Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
Connection: keep-alive
Host: rutgo-letsgo.tistory.com
Origin: https://www.google.com
Referer: https://www.google.com/
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: cross-site
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.198 Safari/537.36
```

**Response 헤더**
```javascript
Access-Control-Allow-Origin: http://rutgo-letsgo.tistory.com
Content-Encoding: gzip
Content-Type: text/xml; charset=utf-8
Date: Fri, 13 Nov 2020 07:37:56 GMT
P3P: CP='ALL DSP COR MON LAW OUR LEG DEL'
Transfer-Encoding: chunked
Vary: Accept-Encoding
X-UA-Compatible: IE=Edge
```

**비교**
```javascript 
Request   | Origin: https://www.google.com
Response  | Access-Control-Allow-Origin: http://rutgo-letsgo.tistory.com
```

# 결론 

# 참고 
블로그 :   
https://evan-moon.github.io/2020/05/21/about-cors/          
https://developer.mozilla.org/ko/docs/Web/HTTP/CORS     
https://developer.mozilla.org/ko/docs/Glossary/Preflight_request     
https://minzoovv.dev/HTTP/cors/   
https://brownbears.tistory.com/336   
https://ko.javascript.info/fetch-crossorigin#ref-561  
동영상 :   
