# XSS
> Cross Site Script    
> 사이트 간 스크립팅       

* 가장 널리 알려진 웹 보안 취약점 중 하나   
* 악의적인 사용자가 공격하려는 사이트에 악성 스크립트를 삽입할 수 있는 보안 취약점이다.   
* XSS를 통해 C&C(Zombie PC에 명령을 내리거나 악성 코드를 제어하는 서버)로 리다이렉트하거나 
사용자의 쿠키를 탈취하여 세션 하이재킹 공격을 할 수 있다.       
* 대표적인 공격 방식 
   * Stored XSS   
   * Reflected XSS  
   * DOM based XSS   

# StoredXSS   
* 공격자가 제공한 데이터가 **서버에 저장된 후**    
지속적으로 서비스를 제공하는 정상 페이지에 **다른 사용자에게 스크립트 노출**되는 기법   

## StoredXSS Flow   

[ 사진 ]   
   
* 해커가 악의적인 스크립트가 담긴 게시물 등록     
  
[ 사진 ]   

* 스크립트가 데이터베이스에 저장     

[ 사진 ]   

* 사용자가 게시물을 읽기 위해 SELECT를 받으면 HTML 문서안에 스크립트가 주입

[ 사진 ]    

* 스크립트 실행  

# Reflected XSS   
* 웹 어플리케이션의 지정된 파라미터를 사용할 때 발생하는 취약점을 이용한 공격법   
* "검색어"와 같은 쿼리스트링을 URL에 담아 전송했을 때,    
서버가 필터링 거치치 않고 쿼리에 포함된 스크립트를 응답 페이지에 담아 전송함으로써 발생   
* 공격용 스크립트가 대상 웹사이트에 있지 않고 다른 매체(타 사이트, 메일)에 포함될 수 있다.   
* Stored XSS와는 다르게 데이터베이스에 스크립트가 저장되지 않고 **응답 페이지에 바로 클라이언트에 전달**되는 차이점이 있다.      

## Reflected XSS Flow     
   
[ 사진 ]   

* 해커가 악의적인 스크립트를 URL에 담아 공유   

[ 사진 ]   

* 사용자가 클릭하면 스크립트가 삽입된 페이지로 연결    

# XSS Example   
## Stored XSS Example
```html 
<script>alert('document.cookie')</script>
```
* 기존 Stored XSS 개념대로라면 DB에 해당 Script 태그가 저장되어 해당 데이터를 GET하면 출력되어야 한다.   
* **하지만** HTML5 는 innerHTML 과 함께 삽입된 <script> 태그가 실행되지 않도록 지정합니다.    
* 여기서 중요한 점은 실행이 되지 않는다는 것이지 해당 코드가 없다는 이야기는 아니다. -> 이후, 이 말을 한 이유가 나온다.   
   
```html 
<img src="" onerror="alert('document.cookie')">     
```   
* HTML5는 innerHTML과 함께 삽입된 <script> 태그가 실행하지 않을 뿐이다.   
* 즉, 다른 방법을 통해 강제적으로 실행시킬 수 있다는 말이다.  
* 특정 동작을 처리하기 위해 이벤트로 script를 넣어주어 이를 강제로 실행하게끔 만들었다.   
* 즉, 위와 같은 코드를 form 요소에 입력하면 데이터를 조회하는 사용자의 쿠키 정보를 실제로 알 수 있다.    

```html
<img src="" onerror="
                     fetch('/article', {
                        method:'POST',
                        headers: {
                          withCredential : true // CROS 자격을 트루라 지정함  
                          'ContentType': 'application/json'   
                        },     
                        body : JSON.stringfy({
                          content: document.cookie,
                          writer: 'hacker'                    
                        })
                     }); ">     
```
* alert 뿐만 아니라 Javascript 문법을 사용할 수 있는 것이므로 서버에 게시글을 저장시킬 수도 있다.   
* 또한, 앞서 말햇듯이 C&C 서버로 리다이렉트시켜 좀비 PC로 만들 수 있다.   






