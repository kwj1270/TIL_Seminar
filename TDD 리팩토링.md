# 발표내용 
1. 의식적인 연습이란?     
2. TDD 리팩토링 적용 - 개인   
3. TDD 리팩토링 적용 - 개인(주니어) -> 팀     
4. TDD 리팩토링 적용 - 내가 리더      
    
# 의식적인 연습이란?         
TDD, 리팩토링을 잘 하려면... **연습 연습 연습**               
그런데 무조건 **연습을 많이 한다고 잘할 수 있을까?**            
             
다시 말하자면 우리가 양치를 매일 하는데 양치를 잘 해졌을까?               
**아니다** 우리는 무의식적으로 그저 양치질만 했을 뿐이지 노하우가 좋아지지는 않았다.         
**즉, 우리가 무엇인가를 연습할 때 무조건 많은 시간을 투자한다고 많은 연습을 한다고 역량이 좋아지지는 않습니다.**         
        
박재성 강의자님도 TDD, 리팩토링과 관련해 5-6년을 도전한 후에야          
      
**테스트 하기 쉬운 코드와 테스트하기 어려운 코드를 보는 눈**         
**테스트 하기 어려운 코드를 테스트 하기 쉬운 코드로 설계하는 감(sense)**       
가 생겼다고 한다.       
         
TDD, 리팩토링. 멋져보인다.           
하지만 생각만큼 쉽게 연습할 수 있는 녀석이 아니다.             
**그렇다면 좀 더 효과적으로 연습할 수 있는 방법은 없을까?**    
  
1만 시간의 재발견이란 책에서 아마추어와 프로의 차이는 **목적이 있는 연습** 에 따라 달렸다고 합니다.   

## 의식적인 연습의 7가지 원칙   
1. 효과적인 훈련 기법이 수립되어 있는 기술 연마     
2. **개인의 컴포트 존을 벗어난 지점에서 진행, 자신의 현재 능력을 살짝 넘어가는 작업을 지속적으로 시도**     
3. **명확하고 구체적인 목표**를 가지고 진행       
4. 신중하고 계획적이다. 즉, 개인이 온전히 집중하고 '의식적'으로 행동할 것을 요구   
5. **피드백과 피드백에 따른 행동 변경**을 수반   
6. 효과적인 심적 표상을 만들어내는 한편으로 심적 표상에 의존   
7. **기존에 습득한 기술의 특정 부분을 집중적으로 개선함으로써 발전시키고 수정**하는 과정을 수반 

컴포트 존 즉, 안전지대를 벗어난 지점에서 진행 : 기존 내 방식이 아닌 무언가 새롭게 하고자 하는 방향성 가져야한다.   
   
**의식적인 연습으로 효과적으로 연습하자**   
     
## 의식적인 연습 예시 - 우테코 프리코스      
### 우테코 프리코스 진행 방식       
* 3주 동안 진행 매주 해결해야할 미션을 부여           
* 미션을 완료한 후 GitHub의 Pull Request(이하 PR)로 제출       
* 각 PR 평가 후 공통 피드백      
* 선발 과정이지만 3주 동안 배움이 있는 과정을 만들자     
    
### 1주차 - 프로그레밍 제약사항   
* 자바 코드 컨벤션을 지키면서 프로그래밍한다.   
    * **참고문서** : https://google.github.io/styleguide/javaguide.html 또는 https://myeonguni.tistory.com/1596   
    앞선 문서는 매일매일 읽어도 보람차다 무조건 읽도록  
    * indent(인덴트, 들여쓰기) depth를 3이 넘지 않도록 구현한다. 2까지만 허용한다.   
        * 예를 들어 while문 안에 if문이 있으면 들여쓰기는 2이다.   
        * 힌트 : indent(인덴트, 들여쓰기) depth를 줄이는 좋은 방법은 함수(메서드)를 분리하면 된다.   
    * 함수(메서드)가 한 가지 일만 하도록 최대한 작게 만들어라   

### 1주차 - 피드백  
* space(공백)도 convention 이다.      
    * for, while, if문 사이의 space도 convention이다.     
* 불필요하게 공백 라인을 만들지 않는다.     
    * 공백 라인을 뛰우는 것도 코드상에 문맥이 달라지는 부분에 의도를 가지고 뛰우면 좋겠다.     
* git commit 메시지를 의미있게 작성한다.     
    * git commit 메시지에 해당 commit에서 작업한 내용에 대한 이해가 가능하도록 작성한다.     
    * 10여개의 피드백    
    
### 2주차 - 프로그레밍 제약사항   
* 자바 코드 컨벤션을 지키면서 프로그래밍한다.   
    * **참고문서** : https://google.github.io/styleguide/javaguide.html 또는 https://myeonguni.tistory.com/1596   
    앞선 문서는 매일매일 읽어도 보람차다 무조건 읽도록  
    * indent(인덴트, 들여쓰기) depth를 3이 넘지 않도록 구현한다. 2까지만 허용한다.   
        * 예를 들어 while문 안에 if문이 있으면 들여쓰기는 2이다.   
        * 힌트 : indent(인덴트, 들여쓰기) depth를 줄이는 좋은 방법은 함수(메서드)를 분리하면 된다.   
    * 함수(메서드)가 한 가지 일만 하도록 최대한 작게 만들어라   
* **함수(메서드)의 길이가 15라인을 넘어가지 않도록 구현한다.**  
    * 함수(메서드)가 한 가지 일만 잘 하도록 구현한다.   
* **else 예약어를 쓰지 않는다.**   
    * 힌트 : if 조건절에서 값을 return하는 방식으로 구현하면 else를 사용하지 않아도 된다.   
    * else를 쓰지 말라고 하니 switch/case로 구현하는 경우도 있는데 이같은 경우도 허용하지 않는다.  
    * 자바 코드 컨벤션을 지키면서 프로그래밍한다.     
      
### 2주차 - 피드백  
* **java api를 적극 활용한다.**     
    * 메소드를 직접 구현하기 전에 java api에서 제공하는 기능인지 검색을 해본다.   
       
예시)    
우승자 ```pobi```와 ```jason``` 2명 이상일 때 ```pobi,jason```으로 출력   
   
```java
List<String> winners = Arrays.asList("pobi", "jason");
String result = String.join(",", winners);
```
```java List String combine``` 또는 ```java List String join``` 검색시 알 수 있더라 단순하게 검색하도록   

### 3주차 - 프로그레밍 제약사항   
* 자바 코드 컨벤션을 지키면서 프로그래밍한다.   
    * **참고문서** : https://google.github.io/styleguide/javaguide.html 또는 https://myeonguni.tistory.com/1596   
    앞선 문서는 매일매일 읽어도 보람차다 무조건 읽도록  
    * **indent(인덴트, 들여쓰기) depth를 2가 넘지 않도록 구현한다. 1까지만 허용한다.**
        * 예를 들어 while문 안에 if문이 있으면 들여쓰기는 2이다.   
        * 힌트 : indent(인덴트, 들여쓰기) depth를 줄이는 좋은 방법은 함수(메서드)를 분리하면 된다.
    * **최대한 1을 유지하기 위해 노력하고, 정말 힘든 경우 2까지 허용한다.**
    * 함수(메서드)가 한 가지 일만 하도록 최대한 작게 만들어라   
* **함수(메서드)의 길이가 10라인을 넘어가지 않도록 구현한다.**  
    * 함수(메서드)가 한 가지 일만 잘 하도록 구현한다.   
* **else 예약어를 쓰지 않는다.**   
    * 힌트 : if 조건절에서 값을 return하는 방식으로 구현하면 else를 사용하지 않아도 된다.   
    * else를 쓰지 말라고 하니 switch/case로 구현하는 경우도 있는데 이같은 경우도 허용하지 않는다.  
    * 자바 코드 컨벤션을 지키면서 프로그래밍한다.       
* **함수(메서드)의 인자수를 3개까지만 허용한다. 4개 이상은 허용하지 않는다.**   
    * 클래스를 만들거나 비슷한 작업을 처리하도록 해야겠다.   
    
### 3주차 - 피드백  
* **객체에 메시지를 보내라**   
    * 상태 데이터를 가지는 객체에서 데이터를 꺼내려 (get) 하지 말고 객체에 메시지를 보내라     
   
**미개선 코드**
```java
private boolean isMaxPosition(Car car){
    return car.getPosition() == maxDistance;
}
```
  
**개선 코드**
```java
private boolean isMaxPosition(Car car){
    return car.isMaxPosition(maxDistance); // 오버로딩으로 처리한 것 같다.  
}
```

# 의식적인 연습으로 TDD 리팩토링 적용 - 개인  
TDD 리팩토링 == 운동          
평생동안 연습하겠다는 마음가지음로 시작           
   
## 시작하기 - 주변 정리해 꾸준히 연습할 시간 확보   
* 애인과의 만남 시간 조정   
* 친구들과의 관계 끊기      
* TV 보지 않기, 게임하지 않기      
     
## 시작하기 - 장난감 프로젝트 찾기       
주변 환경에 영향을 받지 않고 꾸준히 연습하기 위함             
회사 프로젝트로는 X -> 회사 프로젝트로 연습하게 되면 언제 어떤 업무가 0순위로 치고 들어올지 모름    
즉, 바빠서 TDD를 못하게되고 리듬이 깨지게 된다.         
      
## 1단계 - 단위테스트 연습   
**내가 사용하는 API 사용법을 익히기 위한 학습 테스트에서 시작**   
* 자바 String 클래스의 다양한 메서드(함수) 사용법        
* 자바 ArrayList에 데이터를 추가, 수정, 삭제하는 방법    
   
**예시**
```java
import org.junit.Test;

import static org.assertj.core.api.Assertions.asserThat;

public class StringTest{
    @Test
    public void split(){
        String[] values = "1".split(",");
        assertThat(values).contains("1");
        value = "1,2".split(",");
        assertThat(values).containsExactly("1", "2");
    }
    
    @Test
    public void substring(){
        String input = "(1,2)";
        String result = input.substring(1, input.length() - 1);
        asserThat(result).isEqualTo("1,2");
    }
}
```
내가 많이 쓰는 메서드가 어떻게 동작하는지 이런 작은 동작부터 하나하나 단위 테스트를 진행해본다.   

**예시2**
```java
import org.junit.Test;

import java.util.ArrayList;

import static org.assertj.core.api.Assertions.asserThat;

public class CollectionTest {
    @Test
    public void arrayList(){
        ArrayList<String> values = new ArrayList<>();
        values.add("first");
        values.add("second");
        assertThat(values.add("thrid")).isTrue();
        assertThat(values.size()).isEqualTo(3);
        assertThat(values.get(0)).isEqualTo("first");
        assertThat(values.contains("first")).isTrue();
        assertThat(values.remove(0)).isEqualTo("first");
        assertThat(values.size()).isEqualTo(2);
    }
}
```
     
### 연습 효과      
* 단위테스트 방법을 학습할 수 있습니다.        
* 단위테스트 도구 (xUnit)의 사용법을 익힐 수 있다.          
* 사용하는 API에 대한 학습 효과가 있다.         
       
내가 구현하는 메서드(함수) 중         
**Input과 Output이 명확한 클래스 메소드(보통 Util 성격의 메서드)** 에 대한 단위 테스트 연습         
        
## 2 단계 - TDD 연습    
어려운 문제를 해결하는 것이 목적이 아니라 TDD 연습이 목적          
**난이도가 낮거나 자신에게 익숙한 문제로 시작하는 것을 추천**       
            
웹, 모바일 UI나 DB에 의존관계를 가지지 않는 요구사항으로 연습한다.       
  
### 문자열 덧셈 계산기 요구사항      
쉼표```,``` 또는 콜론 ```:```을 구분자로 가지는 문자열을 전달하는 경우 구분자를 기준으로 분리한 각 숫자의 합을 반환      

```
입력                  출력  
null or ""  ->          0
"1"         ->          1
"1,2"       ->          3
"1,2:3"     ->          6
```

![TDD](https://user-images.githubusercontent.com/50267433/79682794-2821da80-8260-11ea-87eb-61cd1eef3b80.png)    
   
    
**테스트 코드**   
```java
public class StringCalculatorTest {
    @Test
    public void null_또는_반값() {
        assertThat(StringCalculator.splitAndSum(null).isEqualTo(0));
        assertThat(StringCalculator.splitAndSum("").isEqualTo(0));
    }
    
    @Test
    public void 값_하나(){
        assertThat(StringCalculator.splitAndSum("1").isEqualTo(1));
    }
    
    @Test
    public void 쉼표_구분자(){
        assertThat(StringCalculator.splitAndSum("1,2").isEqualTo(3));
    }
    
    @Test
    public void 쉼표_콜론_구분자(){
        assertThat(StringCalculator.splitAndSum("1,2:3").isEqualTo(6));
    }
}
```

**프로덕션 코드**
```java
public class StringCalculator {
    public static int splitAndSum(String text) {
        int result = 0;
        if (text == null || text.isEmpty()) {
            result = 0;
        } else {
            String[] values = text.split(",|:");
            for(String value : values) {
                result += Integer.parseInt(value);
            }
        }
        return result;
    }
}
```
  
### 3단계 - 메소드 분리 리팩토링      
테스트 코드는 변경하지 말고     
**테스트 대상 코드(프로덕션 코드)를 개선하는 연습을 집중한다.**     
    
**리팩토링 코드**    
```java
public class StringCalculator {
    public static int splitAndSum(String text) {
        if (text==null || text.isEmpty()) return 0;
        String[] values = text.split(",|:");
        return sum(values);
    }
    private static int sum(String[] values){
        int result = 0;
        for(String value : values) {
            result += Integer.parseInt(value);
        }
        return result;
    }
}
```

## 메서드가 한가지 일만 하기  
```java
public class StringCalculator {
    public static int splitAndSum(String text) {
        if (text==null || text.isEmpty()) return 0;
        String[] values = text.split(",|:");
        return sum(values);
    }
    private static int sum(String[] values){
        int result = 0;
        for(String value : values) {
            result += Integer.parseInt(value);
        }
        return result;
    }
}
```
우선 불필요한 변수 사용과 리턴을 배제하였고        
else 구문을 없애며 작업을 처리하도록 했습니다.           
하지만 위 코드도 리펙토링이 잘 되었다 볼수 없습니다.      
    
왜냐하면 ```sum()``` 을 기준으로         
1. 문자열을 숫자로 처리     
2. 숫자를 누적하여 더하기         
   
라는 2가지 작업을 하기 때문입니다.      

```java

public class StringCalculator {
    public static int splitAndSum(String text) {
        if (text==null || text.isEmpty()) return 0;
        String[] values = text.split(",|:");
        int[] numbers = toInt(values);
        return sum(numbers);
    }
    
    private static int[] toInt(String[] values){
        int[] numbers = new int[values.length];
        for(int i=0; i < values.length; i++){
            numbers[i] = Integer.parseInt(values[i]);
        }
        return numbers;
    }
    
    private static int sum(int[] numbers){
        int result = 0;
        for(int number : numbers) {
            result += number;
        }
        return result;
    }
    
}
```   
언뜻보면 코드가 길어진것 같고 for문이 1번에서 2번으로 올라갔지만           
데이터 크기가 크지 않기 때문에 성능에 크게 영향을 미치지 않습니다.             
        
이렇게 메서드가 한가지 일만 처리하게 한다면 이 메소드들이 재활용 될 수 있습니다.                
왜냐하면 가장 작은 단위로 작게 쪼개져있기 때문에 각 추상화 개념에 맞는 경우 사용할 수 있습니다.        
하지만 위와 같이 2가지 추삭적 개념이 존재하면 2가지 개념을 충족시키지 않는다면 재사용이 불가능합니다.     
      
## 로컬 변수가 필요한가?  
```java

public class StringCalculator {
    public static int splitAndSum(String text) {
        if (text==null || text.isEmpty()) return 0;
        String[] values = text.split(",|:");
        int[] numbers = toInt(values);
        return sum(numbers);
    }

    private static int[] toInt(String[] values){
        int[] numbers = new int[values.length];
        for(int i=0; i < values.length; i++){
            numbers[i] = Integer.parseInt(values[i]);
        }
        return numbers;
    }

    private static int sum(int[] numbers){
        int result = 0;
        for(int number : numbers) {
            result += number;
        }
        return result;
    }

}
```
또한 해당 로직에서 로컬변수가 꼭 필요한가 아닌가를 생각을해서 코드를 줄이도록 노력한다.   


**개선 코드**
```java

public class StringCalculator {
    public static int splitAndSum(String text) {
        if (text==null || text.isEmpty()) return 0;
        return sum(toInt(text.split(",|:")));
    }

    private static int[] toInt(String[] values){
        int[] numbers = new int[values.length];
        for(int i=0; i < values.length; i++){
            numbers[i] = Integer.parseInt(values[i]);
        }
        return numbers;
    }

    private static int sum(int[] numbers){
        int result = 0;
        for(int number : numbers) {
            result += number;
        }
        return result;
    }

}
```

## Compose Method 패턴 적용 
메서드(함수)의 의도가 잘 드러나도록 동등한 수준의 작업을 하는 여러 단계로 나눈다. (추상화 레벨을 똑같이해라)     

```java

public class StringCalculator {
    public static int splitAndSum(String text) {
        if (text==null || text.isEmpty()) return 0;
        return sum(toInt(text.split(",|:")));
    }

    private static int[] toInt(String[] values){
        int[] numbers = new int[values.length];
        for(int i=0; i < values.length; i++){
            numbers[i] = Integer.parseInt(values[i]);
        }
        return numbers;
    }

    private static int sum(int[] numbers){
        int result = 0;
        for(int number : numbers) {
            result += number;
        }
        return result;
    }

}
```
같은 경우 ```splitAndSum()```는 다른 두 메서드와 추상화 레벨이 동일하지 않다.    
이유는 이유는 어떻게 계산하는지에 대한 계산식이 보이기 때문이다. -> 추상화 레벨이 올라간다.      
그렇기에 계산식이 보이지 않게끔 해주어 추상화 레벨을 1단계로 낮추어준다.   

**개선 코드**
```java
public class StringCalculator {
    public static int splitAndSum(String text) {
        if (isBlank(text)) return 0;
        return sum(toInt(split(text)));
    }

    private static boolean isBlank(String text){
        return text==null || text.isEmpty();
    }
    private static String[] split(String text){
        return text.split(",|:");
    }

    private static int[] toInt(String[] values){
        int[] numbers = new int[values.length];
        for(int i=0; i < values.length; i++){
            numbers[i] = Integer.parseInt(values[i]);
        }
        return numbers;
    }

    private static int sum(int[] numbers){
        int result = 0;
        for(int number : numbers) {
            result += number;
        }
        return result;
    }

}
```

## 결과

**미 개선 코드**
```java
public class StringCalculator {
    public static int splitAndSum(String text) {
        int result = 0;
        if (text == null || text.isEmpty()) {
            result = 0;
        } else {
            String[] values = text.split(",|:");
            for(String value : values) {
                result += Integer.parseInt(value);
            }
        }
        return result;
    }
}
```

**개선 코드**
```java
public class StringCalculator {
    public static int splitAndSum(String text) {
        if (isBlank(text)) return 0;
        return sum(toInt(split(text)));
    }

    private static boolean isBlank(String text){
        return text==null || text.isEmpty();
    }
    private static String[] split(String text){
        return text.split(",|:");
    }

    private static int[] toInt(String[] values){
        int[] numbers = new int[values.length];
        for(int i=0; i < values.length; i++){
            numbers[i] = Integer.parseInt(values[i]);
        }
        return numbers;
    }

    private static int sum(int[] numbers){
        int result = 0;
        for(int number : numbers) {
            result += number;
        }
        return result;
    }

}
```
이제 두 코드를 살펴보자       
만약 내가 해당 코드및 로직을 알지 못한다는 가정하에 처음 이 코드를 접했다면 어떤 코드가 이해하기 쉬울까?        
단순히 강의에서 말해서가 아니라 객관적으로 2번째 코드가 좋다고 말할 수 있다.          
이유는 1번째는 내가 로직을 하나하나 따라가면서 처리해야하지만         
2번째는 메서드의 이름만 보고도 내가 그 로직을 보지 않더라도 유추가 가능하기 때문이다.      
      
일단 주제인 연습에 관한 결론을 말하자면      
**한번에 모든 원칙을 지키면서 리팩토링하려고 연습하지 마라**         
**한번에 한 가지 명확하고 구체적인 목표를 가지고 연습하라**     
  
  
