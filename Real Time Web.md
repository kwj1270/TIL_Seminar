# Realtime Web
> 실시간 웹을 구현하는 기술   

# 목차
1. Realtime Web이란?   
2. Realtime Web을 구현하는 기술   
  1. Polling 
  2. Long Polling  
  3. Server-sent events
  4. Web Socket   
3. 기술 선택  

# Realtime Web이란?     
> 인터넷에서 사용자들로 하여금 창작자가 정보를 만들어내는 즉시 수신할 수 있도록하는 기술 혹은 서비스     
   
**전통적인 웹**        
* 웹은 HTTP 요청-응답 모델을 기반으로 구축됐다.         
* HTTP는 무상태 프로토콜이며 클라이언트와 서버 간의 통신은 각각의 독립적인 요청과 응답의 쌍으로 구성된다.     
* 웹 브라우저에서 폼을 채우고 이를 웹 서버로 제출하는 하나의 요청으로       
웹 서버는 요청된 내용에 따라서 데이터를 가공하여 새로운 웹페이지를 작성하고 응답으로 되돌려준다.      
     
이 같은 형태를 `포스트 백`이라 하는데 요청이 있을 때마다 페이지를 새로 그리는 작업을 한다.      
    
**AJAX의 등장**    
* 사용자 인터페이스 나머지 부분을 방해하지 않고 비동기로 데이터를 송/수신 할 수 있다.      
* 전체 페이즈를 다시 로딩하는 것이 아닌 일부분만 변경하기 때문에 빠른 화면 전환이 가능하다.  

# Realtime Web을 구현하는 기술   
## Polling - 주기적인 요청   
* 전송할 데이터의 유무에 관계없이 주기적으로 요청을 수행하는 방법이다.        
* 클라이언트는 지정된 시간 간격에 맞춰 서버에 지속적인 요청을 보낸다.        
* 서버는 각 요청마다 가용 데이터나 데이터가 없는 경우 빈 데이터를 보내거나 실패와 같은 적절한 응답을 한다.   
   
<img width="837" alt="스크린샷 2020-11-20 오후 3 23 54" src="https://user-images.githubusercontent.com/50267433/99766486-8b505400-2b44-11eb-8acf-0226b70f470b.png">   
   
* 매 시간마다 주기적으로 요청을 보낸다.   
* 요청 전에 이벤트가 발생하지 않았더라도 (가용 데이터가 없더라도) 응답을 해줍니다.  
* 요청 전에 이벤트가 발생하면 (가용 데이터 존재) 해당 데이터를 통한 응답을 해줍니다.   

```javascript  
const delay = (ms) => new Promise((resolve) => setTimeout(resolve, ms))

const fetchPosts = (cursor) =>
  fetch('/api/posts?cursor=&{cursor}')
    .then((response) => response.json())
    .then(prependPosts)
   
async function polling() {
  while (true) {
    await delay(1000)  
    await fetchPosts($posts.firstElementChild.dataset.postId)
  }
}   

fetchPosts(0).then(polling)      
```
