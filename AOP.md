# AOP
> 기존 kwj1270이 정리했던 AOP-(AspectJ):  https://github.com/kwj1270/TIL_SPRING_QUICK_START/blob/master/%EC%A0%95%EB%A6%AC/09%20AOP%20%EC%9A%A9%EC%96%B4%20%EB%B0%8F%20%EA%B8%B0%EB%B3%B8%20%EC%84%A4%EC%A0%95.md    
   
## 시나리오
### TAKE_1
   
```
선배 개발자 : 회원가입 하는 시간 좀 측정해서 로그로 남겨줄 수 있어요?   
개발자 : ok
```

**기존 코드**
```java
public void join(JoinRequest joinRequest) {
  memberRepository.save(joinRequest.toMember());
}
```

**개발자가 작성한 코드 - 일반 버전**
```java
public void join(JoinRequest joinRequest) {
  long begin = System.currentTimeMillis();
  try {
    memberRepository.save(joinRequest.toMember());
  } finally {
    log.info("join spen {} ms", System.currentTimeMills() - begin);
  }
}
```

**개발자가 작성한 코드 - 객체지향 버전**
```java
public void join(JoinRequest joinRequest) {
  StopWatch stopWatch = new StopWatch();
  stopWatch.strat();
  try {
    memberRepository.save(joinRequest.toMember());
  } finally {
    stopWatch.stop();
    log.info("join spen {} ms", stopWatch.getLastTaskTimeMillis());
  }
}
```

### TAKE_2
   
```
선배 개발자 : 오케이 정말 잘했어요 그럼 이 코드를 모든 서비스에 적용시켜줄래요?   
개발자 : ....?!
사실 서비스는 1억개이며 여기에 있는 메서드들도 각각 1억개라고 한다면?     
```    

* 로깅 같은 작업은 개발에 있어서 중요한 작업이지만 만약 무수히 많은 클래스에서 사용한다면 이를 관리할 수 있을까?   
* 아니 다시 말하자면, 단순 반복되면서 사용되는 코드를 모든 코드에 각각 기술해서 사용해야 할까?     
  
**개발자가 작성한 코드 - 객체지향 버전**
```java
public void join(JoinRequest joinRequest) {
  StopWatch stopWatch = new StopWatch();
  stopWatch.strat();
  try {
    memberRepository.save(joinRequest.toMember());
  } finally {
    stopWatch.stop();
    log.info("join spen {} ms", stopWatch.getLastTaskTimeMillis());
  }
}
```
* 우리는 생각해야하한다.    
* 각각의 메서드는 1가지 기능만 수행해야 한다.   
* 또한, Service 클래스와 그 메서드의 본질적인 역할은 **비즈니스 로직을 처리하는 것**이지 로깅을 하는 것이 아니다.   
* 오히려 위 코드가 삽입되면서 비즈니스 로직에 대한 가독성은 줄어들고 관리해야할 코드는 늘었다.   
  * 핵심 기능 : 비지니스 로직 
  * 부가 기능 : 로깅 로직  
* 그렇다면 로깅 메서드를 분리해서 이를 사용하는 방법을 사용할까?   
  * 나쁘지 않다! 하지만 좋지도 않다.

## 부가 기능   
> 인프라 로직  

**인프라 로직**      
- 애플리케이션의 전 영역에서 나타날 수 있다. 
- 중복 코드를 만들어낼 가능성 때문에 유지보수가 힘들어짐   
- 비즈니스 로직과 함께 있으면 비즈니스 로직을 이해하기 어려워짐   

<img width="1282" alt="스크린샷 2020-11-16 오후 1 05 46" src="https://user-images.githubusercontent.com/50267433/99211839-a4879680-280c-11eb-897d-c2970351f3bb.png">   
    
* 성능 검사  
* 로깅 
* 비즈니스 로직 
* 권한 체크      
     
위와 같은 부가적인 기능들이 각각의 핵심 기능위에 블록을 쌓듯이 중복되어 존재하는 것을 알 수 있습니다.      
또한 같은 블록을 동일 선상에 두어보면 횡단하는 듯한 모습 또한 볼 수 있습니다.     
    
<img width="1285" alt="스크린샷 2020-11-16 오후 1 06 43" src="https://user-images.githubusercontent.com/50267433/99211873-b9fcc080-280c-11eb-8c39-d98b7dd63e80.png">
     
* **cross-cutting concern :** 부가적인 기능인 인프라 로직이 중복되어 횡단(가로)과 같은 모습을 나타내는 로직      
* **core concern :** 사용자의 요청에 따라 실제로 수행되는 핵심 비즈니스 로직        

# AOP에 대해서  
> Aspect-Oriented Programming | 관점 지향 프로그래밍   
   
* OOP 객체지향 프로그램   
* AOP 관점지향 프로그램    
    
AOP는 OOP를 더욱 OOP답게 프로그래밍 할 수 있게 도와주는 것으로    
애플리케이션의 핵심적인 기능과 부가적인 기능을 분리해, Aspect라는 모듈로 만들어 설계하고 개발하는 방법이다.    
    
예를 들면 캡슐화된 어떠한 클래스를 대상으로 핵심기능과 부가적인 기능의 관점으로    
공통으로 사용하는 부가적인 기능들을 외부의 독립된 클래스로 분리하고, 이를 모듈화하여 재사용할 수 있게끔 하는 프로그래밍 기법입니다.    
   
실제로 Spring doc document 에서는 아래와 같이 말하고 있습니다.  
```   
Aspect-oriented Programming (AOP) complements    
Object-oriented Programming (OOP) by providing   
another way of thinking about program structure   

AOP는 프로그램 구조에 대한 다른 생각의 방향을 제공해주면서 OOP를 보완하고 있다.       
```      

# AOP 용어 
- **Target :** 
  - AOP의 대상   
- **Advice :** 
  - AOP 메서드 : AOP 적용시에 사용되는 메서드 (부가 기능 로직 메서드)              
  - 부가 기능은 물론 적용 시점까지도 지정할 수 있다.         
      - Before, AfterReturning, AfterThrowing, After, Around    
- **Join point :** 
  - AOP가 적용될 수 있는 메소드이다.   
  - **메소드**, 필드, 객체, 생성자 등 (Spring AOP에서는 메서드만 가능)    
- **Point cut :**    
  - AOP가 적용될 수 있는 모든 Element들에서 실제 사용하고자 지정된 몇 개를 의미 (전체 중 사용될 일부를 의미)       
  - 즉, Join point에서 실제 advice가 적용될 몇 개의 지점, Spring AOP 에서는 advice가 적용될 메서드를 선정       
- **Weaving :**   
   - Point cut으로 지정된 요소가 호출될 때 어드바이스 메서드(AOP메서드)가 호출되는 과정을 의미    
   - 즉, Point cut 으로 지정한 핵심 관심 메서드가 호출될 때, 어드바이스에 해당하는 횡단 관심 메서드가 삽입되는 과정을 의미한다.
   - Weaving 처리 방식
      - 컴파일타임 위빙 : a.java -> a.clss
      - 로딩타임 위빙 : a.class 를 메모리에서 로드할 때   
      - 런타임 위빙 :

# 참고 : 
https://devbox.tistory.com/entry/spring-AOP-%EC%9A%A9%EC%96%B4-%EC%84%A4%EB%AA%85


# Spring AOP 사용   
