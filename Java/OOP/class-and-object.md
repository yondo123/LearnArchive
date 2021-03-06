## 객체지향언어
### 객체지향언어의 장점?
+ 재사용성
+ 유지보수 용이
+ 중복코드 축소

### 객체와 인스턴스
+ **객체**
    - 클래스로부터 객체를 만드는 과정을 클래스의 인스턴스화라고 한다.

+ **인스턴스**
    - 클래스로부터 만들어진 객체를 해당 클래스의 인스턴스(instance)라고 한다.

+ **클래스**
    - 객체를 정의해 놓은 것

+ **실습**
```java
    //계산기 객체 (클래스)
    class Calculator {
        // 계산기 속성 (멤버변수)
        int firstOperand; // 피연산자1
        int secOperand; // 피연산자2

        // 계산기 기능(메소드)
        void sum() {
            System.out.println("덧셈결과:" + (this.firstOperand + this.secOperand));
        }

        void div() {
            System.out.println("나눗결과:" + (this.firstOperand / this.secOperand));
        }

        void sub() {
            System.out.println("뺄셈결과:" + (this.firstOperand - this.secOperand));
        }

        void multiple() {
            System.out.println("곱셈결과: " + (this.firstOperand * this.secOperand));
        }
    }

    class CalculatorExecute {
        public static void main(String[] args) {
            Calculator cal = new Calculator();
            cal.firstOperand = 3;
            cal.secOperand = 4;
            
            cal.sub();
            cal.div();
            cal.sum();
            cal.multiple();
        }
    }

```

### 객체배열
+ 많은 수의 객체를 다뤄야 할 때 유용하게 사용할 수 있다.
+ 배열안에 객체를 담는다고 해서 객체 자체가 저장되는것이 아니라, `객체의 주소`가 담기게 된다.

+ **실습**
```java
class arrayCalculator {
	public static void main(String[] args) {
		Calculator[] calArray  = new Calculator[3]; //length 3인 객체 배열 생성 (null)
		for(int i=0; i < calArray.length; i++) {
			calArray[i] = new Calculator();
			calArray[i].firstOperand = i;
			calArray[i].secOperand = calArray.length - i;
			calArray[i].sum();
			calArray[i].sub();
			calArray[i].multiple();
			calArray[i].div();
		}
	}
}

//계산기 객체 (클래스)
class Calculator {
  // 계산기 속성 (멤버변수)
  int firstOperand; // 피연산자1
  int secOperand; // 피연산자2

  // 계산기 기능(메소드)
  void sum() {
      System.out.println("덧셈결과:" + (this.firstOperand + this.secOperand));
  }

  void div() {
      System.out.println("나눗결과:" + (this.firstOperand / this.secOperand));
  }

  void sub() {
      System.out.println("뺄셈결과:" + (this.firstOperand - this.secOperand));
  }

  void multiple() {
      System.out.println("곱셈결과: " + (this.firstOperand * this.secOperand));
  }
}
```
### 클래스메소드와 인스턴스메소드
+ **클래스메소드**
    + 메소드 앞에 `static`이 붙는 메소드, 객체를 생성하지 않고 호출이 가능하다.
    + 클래스가 메모리에 올라갈 때 이미 생성된다.

+ **인스턴스메소드**
    + 객체를 생성해야 호출할 수 있는 메소드, `인스턴스 변수가 필요한 상황`이면 필요로하는 메소드이다.

+ **실습(위 계산기 예제로 한 클래스메소드&&인스턴스메소드 사용)**
```java
    class calculatorTest{
        long a, b; //인스턴스 변수 선언
        
        //인스턴스 메소드(매개변수 필요 x)
        long add(){ return a+b; }
        long div() {return a / b;}
        long mul() {return a * b;}
        long sum() {return a - b;}
        
        //클래스 메소드(계산하기 위한 매개변수가 필요)
        static int add(int a, int b) { return a + b;}
        static long div(int a, int b) {return a / b;}
        static int mul(int a, int b){return a * b;}
        static int sum(int a, int b) {return a - b;}
    }

    public class instanceAndClass {
        public static void main(String[] args) {
            System.out.println("더하기 : "+calculatorTest.add(3, 5)); //클래스 메소드 호출 (인스턴스 생성 필요없음)
            
            calculatorTest cal = new calculatorTest(); //인스턴스 메소드를 실행하기 위한 인스턴스 생성
            cal.a = 5;
            cal.b = 3;
            System.out.println("나누기 "+cal.div());
        }
    }
```

### 클래스멤버-인스턴스멤버 참고간 주의사항
+ 클래스멤버(클래스메소드, 클래스변수)는 인스턴스멤버(인스턴스메소드, 인스턴스변수) 존재 시점에 항상 존재하지만, 역으로 인스턴스멤버는 클래스멤버가 존재하는 시점에 항상 존재하는 것은 아니다.
+ 인스턴스 멤버는 반드시 객체를 생헝한 후에 참조 및 호출이 가능하기 때문에, 객체를 생성해야만 한다.
+ 인스턴스 멤버들 사이에서는 서로 다른 인스턴스 멤버들을 호출하는 데 전혀 문제가 없다. `하나의 인스턴스가 존재하는것은 선언한 다른 인스턴스도 존재한다는 의미이다.`