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
    * 코드를 추가하거나 수정할 위치를 찾는데 점점 오랜 시간이 걸린다.
* if-else 를 추가하면 변경해줘야 할 메서드가 있을 수 있고 수정하는 작업을 누락할 수 있다.  
* 또한, 사용되는 상수 추가, 수정, 삭제에 관한 관리를 해주어야 한다는 문제점이 있다.  

# OCP란?
* 객체지향의 5대 원칙 **-SOLID 원칙-**
    * SRP : 단일 책임 원칙 - 모든 클래스는 각각 하나의 책임만 가져야 한다. 
    * OCP : 개방 폐쇄 원칙 - 기존의 코드를 변경하지 않으면서(Closed), 기능을 추가할 수 있도록(Open) 설계가 되어야 한다는 원칙
    * LSP : 리스코프 치환 원칙 - 자식 클래스는 언제나 자신의 부모 클래스를 대체할 수 있다는 원칙이다.
    * ISP : 한 클래스는 자신이 사용하지않는 인터페이스는 구현하지 말아야 한다. 
    * DIP : 의존 역전 원칙 - 구체적인 클래스보다 인터페이스나 추상 클래스와 관계를 맺어야 한다.   
    
**OCP**     
소프트웨어 구성 요소(컴포넌트, 클래스, 모듈, 함수)는 **확장에 대해서는 개방**돼야 하지만 **변경에 대해서는 폐쇄**되어야 한다.        
**기존의 코드를 변경하지 않으면서** 기능을 추가할 수 있또록 설계가 되어야 한다는 뜻이다.        
   
변경에 대해서 폐쇠되어야 한다 -> 기존의 코드를 변경시키지 않고 유지한 상태로 동작해야한다.    

## 적용 방법
1. 상속 (IS-A) : extends    
**깨지기 쉬운 상위 클래스**       
상속은 하위 클래스가 상위 클래스의 기능과 밀접하기 때문에 상위가 바뀌면 하위에 영향이 매우 크다.     
이는 상속의 장점이자 단점이다.     
    
2. 컴포지션(HAS-A) : implements       
    1. 변경(확장)될 것과 변하지 않을 것을 엄격히 구분      
    2. 이 두 모듈이 만나는 지점에 인터페이스를 정의      
    3. 구현에 의존하기 보단 정의한 인터페이스에 의존하도록 코드를 작성      
    
### 1. 변경(확장)될 것과 변하지 않을 것을 엄격히 구분         
```java
public class LottoNumberAutoGenerator {
  
  // 변경이 되지 않는 코드 //
  public List<Intenger> generate(int shuffle) {
    List<Integer> numbers = new ArrayList<>();
    for(int i=LottoNumber.MIN; i <= LottoNumber.MAX; i++){
      numbers.add(i);
    }
  /////////////////////  
  
  // 변경이 일어나는 코드 // 
  if(shuffle == RANDOM){
      Collections.Shuffle(numbers);
  } else if(shuffle == NOTHING){
      Collections.sort(numbers);
  } else if(shuffle == REVERSE){
      Collections.reverse(numbers);
  }
  /////////////////////
  
  // 변경이 일어나지 않는 코드 // 
  return numbers.subList(0. Lotto.LOTTO_NUMBER_SIZE);
  /////////////////////
  
  }
}
```
* 변경이 일어나는 코드를 인터페이스로 추출하는 과정을 진행하면 된다.    
   
### 2. 모듈이 만나는 지점에 인터페이스 정의   
<img width="832" alt="스크린샷 2020-11-11 오후 2 36 26" src="https://user-images.githubusercontent.com/50267433/98773008-5b5dce00-242b-11eb-9f09-149c6710d370.png">

```java
@FunctionalInterface
public interface ShuffleStrategy{
    public List<Integer> shuffle(List<Integer> numbers);
}
```
* 인터페이스가 LottoNumberAutoGenerator 와 인터페이스 메서드 구현 클래스들을 이어주는 역할      

### 3. 구현에 의존하기 보단 정의한 인터페이스에 의존하도록 코드를 작성
* 인터페이스에 의존해야지 다른 것에 의존하면 안 된다.             
* 즉, LottoNumberAutoGenerator 가 구현 클래스를 직접 의존하면 안 된다.        
        
**좋지 않은 코드**   
```java
public class LottoNumberAutoGenerator {
  private final ShuffleRandomStrategy shuffleRandomStrategy; // 구현 클래스 직접 의존
    
  public LottoNumberAutoGenerator(ShuffleRandomStrategy shuffleRandomStrategy){
    this.shuffleRandomStrategy = shuffleRandomStrategy;
  }
  
  public List<Intenger> generate(int shuffle) {
    List<Integer> numbers = new ArrayList<>();
    for(int i=LottoNumber.MIN; i <= LottoNumber.MAX; i++){
      numbers.add(i);
    }
  
  numbers = shuffleRandomStrategy.shuffle(numbers); // 구현 클래스의 메서드 사용 
  
  return numbers.subList(0. Lotto.LOTTO_NUMBER_SIZE);
  
  }
}
```
* 위와 같이 진행할 경우 OCP 및 DIP의 원칙을 위배한다.     
* 기능을 변경하고자 한다면 해당 코드를 변경해야하는데 만약 100개 이상이라면? -> 끔찍      
* 그렇기 때문에 인터페이스 의존성을 지니게하여 코드의 변경을 유발하지 않아야한다.     
     
**개선 코드**  
```java
public class LottoNumberAutoGenerator {
  private final ShuffleStrategy shuffleStrategy; // 인터페이스 의존 -> 관련 구현 클래스들을 받을 수 있고 변경하지 않아도 됨   
    
  pulic LottoNumberAutoGenerator(ShuffleStrategy shuffleStrategy){
    this.shuffleStrategy = shuffleStrategy;
  } 
    
  public List<Intenger> generate(int shuffle) {
    List<Integer> numbers = new ArrayList<>();
    for(int i=LottoNumber.MIN; i <= LottoNumber.MAX; i++){
      numbers.add(i);
    }
  
  numbers = shuffleStrategy.shuffle(numbers); // 참조하고 있는 인스턴스에 맞는 shuffle 메서드 실행 -> 내부 로직 몰라도 됨 -> 추가로 이름 잘 지어야하는 이유 중 하나이기도  
  
  return numbers.subList(0. Lotto.LOTTO_NUMBER_SIZE);
  
  }
}
```
* 참조 대상이 바뀌더라도 코드를 변경할 일이 없다.   
* 또한 처리 로직을 내부로 숨길 수 있다. -> 대신 이름을 잘 지어야한다.   

### 3. 전체 코드

**LottoNumberAutoGenerator - class**
```java
public class LottoNumberAutoGenerator {
  private final ShuffleStrategy shuffleStrategy; // 인터페이스 의존 -> 관련 구현 클래스들을 받을 수 있고 변경하지 않아도 됨   
    
  pulic LottoNumberAutoGenerator(ShuffleStrategy shuffleStrategy){
    this.shuffleStrategy = shuffleStrategy;
  } 
    
  public List<Intenger> generate(int shuffle) {
    List<Integer> numbers = new ArrayList<>();
    for(int i=LottoNumber.MIN; i <= LottoNumber.MAX; i++){
      numbers.add(i);
    }
  
  numbers = shuffleStrategy.shuffle(numbers); // 참조하고 있는 인스턴스에 맞는 shuffle 메서드 실행 -> 내부 로직 몰라도 됨 -> 추가로 이름 잘 지어야하는 이유 중 하나이기도  
  
  return numbers.subList(0. Lotto.LOTTO_NUMBER_SIZE);
  
  }
}
```
   
**ShuffleStrategy - interface**    
```java
@FunctionalInterface
public interface ShuffleStrategy{
    public List<Integer> shuffle(List<Integer> numbers);
}
```

**ShuffleRandomStrategy - class implements interface**    
```java
pulblic class ShuffleRandomStrategy implements ShuffleStrategy {
    private static ShuffleRandomStrategy shuffleRandomStrategy = new ShuffleRandomStrategy();
    
    private ShuffleRandomStrategy(){}
    
    public static ShuffleRandomStrategy getInstance(){
        return instance;
    }
    
    public List<Integer> shuffle(final List<Integer> numbers){
        Collections.shuffle(numbers);
        return numbers;
    }
}
```

**ShuffleReverseStrategy - class implements interface**    
```java
pulblic class ShuffleReverseStrategy implements ShuffleStrategy {
    private static ShuffleReverseStrategy shuffleReverseStrategy = new ShuffleReverseStrategy();
    
    private ShuffleReverseStrategy(){}
    
    public static ShuffleReverseStrategy getInstance(){
        return instance;
    }
    
    public List<Integer> shuffle(final List<Integer> numbers){
        Collections.reverse(numbers);
        return numbers;
    }
}
```

**ShuffleNothingStrategy - class implements interface**    
```java
pulblic class ShuffleNothingStrategy implements ShuffleStrategy {
    private static ShuffleNothingStrategy shuffleNothingStrategy = new ShuffleNothingStrategy();
    
    private ShuffleNothingStrategy(){}
    
    public static ShuffleNothingStrategy getInstance(){
        return instance;
    }
    
    public List<Integer> shuffle(final List<Integer> numbers){
        Collections.sort(numbers);
        return numbers;
    }
}
```

**main - Method exe class**
```java
class Main{
    public static void main(String[] args){
        LottoNumberAutoGenerator lottoNumberAutoGenerator = new LottoNumberAutoGenerator(ShuffleRandomStrategy.getInstance());
        // LottoNumberAutoGenerator lottoNumberAutoGenerator = new LottoNumberAutoGenerator(ShuffleReverseStrategy.getInstance());
        // LottoNumberAutoGenerator lottoNumberAutoGenerator = new LottoNumberAutoGenerator(ShuffleNothingStrategy.getInstance());
    }
}
```




   

