#### 생성자와 소멸자



**생성자**

---

<br>

> 객체를 생성할때 호출되는 메소드

<br>

```c#
[기본형식]

class 클래스명 {
	[접근 제한자] 클래스명(매개변수..) //생성자와 클래스명이 똑같음, 매개변수 O
	{
		//
	}
	
	..
}

//특정값 반환 X
```

<br>

> 우리가 생성자를 만들지 않아도 자동으로 기본 생성자가 생성된다

<br>

*ex)*

```c#
using System;
namespace ConsoleApplication2
{
	class Car
	{
		private int maxSpeed;
		private int speed = 0;
		private string model;
		
		public Car(int maxSpeed, string model) //생성자
		{
			this.maxSpeed = maxSpeed;
			this.model = model;
		}
		public void ShowCarInformation()
		{
			Console.WriteLine(model + "의 현재 속도: " + speed + "km/h, 최대 속도: " + 					maxSpeed + "km/h");
		}
		public void speedUp(int increment)
		{
			if (speed + increment > maxSpeed)
			Console.WriteLine("최대 속도 " + maxSpeed + "km/h를 넘길 수 없습니다.");
			//제한이 걸려있어 325를 넘길 수 없다는 문구가 출력
			else
			{
				speed += increment;
				Console.WriteLine(model + "의 현재 속도는 " + speed + "km/h 입니다.");
			}
		}
		public void speedDown(int decrement)
		{
			if (speed - decrement < 0)
			Console.WriteLine("속도는 0 아래로 떨어질 수 없습니다.");
			
			else
			{
				speed -= decrement;
				Console.WriteLine(model + "의 현재 속도는 " + speed + "km/h 입니다.");
			}
		}
	}
	class Program
	{
		static void Main(string[] args)
		{
			Car car = new Car(325, "람보르기니 가야르도"); //객체생성할때 호출과 초기화를 동시!
			car.ShowCarInformation(); //현제 Car.maxSpeed가 325인상태
			car.speedUp(50); //Car.Speed가 50인상태
			car.speedUp(40); //Car.Speed가 90인상태
			car.speedUp(210); //Car.Speed가 300인상태
			car.speedUp(30); //Car.Speed가 330인상태
 	   }
	}
}
```

<br>

결과:

```
람보르기니 가야르도의 현재 속도: 0km/h, 최대 속도: 325km/h
람보르기니 가야르도의 현재 속도는 50km/h 입니다.
람보르기니 가야르도의 현재 속도는 90km/h 입니다.
람보르기니 가야르도의 현재 속도는 300km/h 입니다.
최대 속도 325km/h를 넘길 수 없습니다.

계속하려면 아무 키나 누르십시오 . . .
```

<br>

> 추가 

<br>

생성자 오버로딩 가능

```c#
class MyClass
{
	public MyClass()
	{
		Console.WriteLine("매개변수가 없는 디폴트 생성자");
	}
	public MyClass(int a)
	{
		Console.WriteLine("정수형 매개변수");
	}
	public MyClass(double d)
	{
		Console.WriteLine("실수형 매개변수");
	}
}
```

<br>

**소멸자**

---

<br>

> 소멸자는 객체를 소멸시킬 때 호출되는 메소드

<br>

````c#
[기본형식]

class 클래스명 {

	~클래스명()//클래스 이름앞에 ~기호
	{
	//
	}
	..
	
}
//상속, 오버로드 X 사용자 호출불가능
````

<br>

*ex)*

```c#
using System;
namespace ConsoleApplication2
{
	class MyClass
	{
		private string name;
        
		public MyClass(string name)
		{
			this.name = name;
			Console.WriteLine(name + " 객체 생성!");
		}
		~MyClass()
		{
			Console.WriteLine(name + " 객체 소멸!");
		}
    }
	class Program
	{
		static void Main(string[] args)
		{
			MyClass ma = new MyClass("A");
			MyClass mb = new MyClass("B");
			MyClass mc = new MyClass("C");
            //가비지 컬랙터가 언제 어떤 순서로 소멸시킬지 모름, 순서 변동가능
		}
	}
}
```

<br>

결과:

```c#
A 객체 생성!
B 객체 생성!
C 객체 생성!

C 객체 소멸!
B 객체 소멸!
A 객체 소멸!

계속하려면 아무 키나 누르십시오 . . .
```

<br>

> 추가

- 소멸자는 생성자와 달리 `*가비지 컬렉터`에 의해 객체가 소멸하는 시점을 판단!

- 하지만 굳이 사용안해도 `가비지컬렉터가 자동`으로 처리 가능

 <br>

  **가비지 컬랙터란?**

효율적인 메모리 관리를 위해 더이상 쓰지않는 객체를 수거함(강제종료?)

