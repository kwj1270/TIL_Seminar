# OCP와 전략 패턴 
> Open-Closed Principle : 개발 폐쇄 원칙       
> 영상 참고 | 우아한 테크코스 | url : https://www.youtube.com/watch?v=90ZDvHl8ROE     
    
(if-else의 문제점)[]   
(OCP)[]   
(전략 패턴)[]   
(연습 문제 추천)[]   

# if-else의 문제점    
- 변경 확장이 될 수록 코드가 복잡해진다.     
- 코드를 수정하거나 수정할 위치를 찾는데 점점 오래 걸린다.    
- 실수로 추가하지 않고 누락하는 부분이 생길 가능성이 있다.      
   
```
if-else 는 조건문이자 분기점이라는 표현을 많이 사용한다.     
좋게 표현하자면 기존보다 2배 많은 분기를 나타낼 수 있지만     
반대로, 기존보다 2배 많은 로직을 관리하고 처리해야한다.    
```

## 오토 로또 생성 코드  

**첫 구현 당시**
```java
public class LottoNumberAutoGenerator {
  
  public List<Intenger> generate() {
    List<Integer> numbers = new ArrayList<>();
    for(int i=LottoNumber.MIN; i <= LottoNumber.MAX; i++){
      numbers.add(i);
    }
    
    Collections.Shuffle(numbers);
    return numbers.subList(0. Lotto.LOTTO_NUMBER_SIZE);
  }
}
```
* 우선 이런 방법이 있었구나 감탄했다.   
  * 프로그래밍은 현실세계를 추상화한것이다.
  * 실제 로또 프로그램 처럼 동작을 하는 것이 어쩌면 가장 바람직할 수도 있다.  
      * 필자는 LinkedHashSet 을 이용했는데 그 방법은 중복이 나올 수 있으므로 `10^3`보다 많은 계산량이 필요하다.    

**두번째 구현 당시 - 기능 추가**
```java
public class LottoNumberAutoGenerator {
  
  public List<Intenger> generate(int shuffle) {
    List<Integer> numbers = new ArrayList<>();
    for(int i=LottoNumber.MIN; i <= LottoNumber.MAX; i++){
      numbers.add(i);
    }
    
    // RANDOM, NOTHING, REVERSE 는 클래스 내에 정해진 상수로 매개변수로 들어온 shuffle과 비교하여 분기를 나눈다.    
    if(shuffle == RANDOM){
        Collections.Shuffle(numbers);
    } else if(shuffle == NOTHING){
        Collections.sort(numbers);
    } else if(shuffle == REVERSE){
        Collections.reverse(numbers);
    }
    
    return numbers.subList(0. Lotto.LOTTO_NUMBER_SIZE);
  }
}
```
**세번째 구현 당시 - 기능 추가**
```java
public class LottoNumberAutoGenerator {
  
  public List<Intenger> generate(int shuffle) {
    List<Integer> numbers = new ArrayList<>();
    for(int i=LottoNumber.MIN; i <= LottoNumber.MAX; i++){
      numbers.add(i);
    }
    
    if(shuffle == RANDOM){
        Collections.Shuffle(numbers);
    } else if(shuffle == NOTHING){
        Collections.sort(numbers);
    } else if(shuffle == REVERSE){
        Collections.reverse(numbers);
    } else if(shuffle == TEN_TO_TWENTY){
        tenShuffle(numbers);
    } else if(shuffle == TEN_TO_TWENTY){
        twentyShuffle(numbers);
    }
    return numbers.subList(0. Lotto.LOTTO_NUMBER_SIZE);
  }
}
```
**네번째 구현 당시 - 기능 추가**
```java
public class LottoNumberAutoGenerator {
  
  public List<Intenger> generate(int shuffle) {
    List<Integer> numbers = new ArrayList<>();
    for(int i=LottoNumber.MIN; i <= LottoNumber.MAX; i++){
      numbers.add(i);
    }
    
    if(shuffle == RANDOM){
        Collections.Shuffle(numbers);
        doSomethingA(numbers);
    } else if(shuffle == NOTHING){
        Collections.sort(numbers);
        doSomethingB(numbers);
    } else if(shuffle == REVERSE){
        Collections.reverse(numbers);
        doSomethingC(numbers);
        doSomethingA(numbers);
    } else if(shuffle == TEN_TO_TWENTY){
        tenShuffle(numbers);
        doSomethingF(numbers);
        doSomethingB(numbers);
    } else if(shuffle == TEN_TO_TWENTY){
        twentyShuffle(numbers);
    }
    return numbers.subList(0. Lotto.LOTTO_NUMBER_SIZE);
  }
}
```   
   
* `계속되는 기능 추가 -> 복잡도 증가 -> 추가, 수정이 힘들어진다.`     
* 이 같이 기능이 늘어날 수록 코드의 길이가 무수히 증가되고 가독성 또한 매우 안 좋아진다.     
* 이로 인해 코드를 추가하거나 수정할 위치를 찾는데 점점 오랜 시간이 걸린다.    
* 그리고 여기서 사용된 상수, 로직을 다 관리해야한다는 문제점이 있다.      

