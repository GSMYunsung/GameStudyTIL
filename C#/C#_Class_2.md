#### C# 클래스의 상속_2



**메소드 재정의(virtual, override)**

---



부모 클래스의 메소드를 자식 클래스에서 다시 정의하고 싶을때 사용한다.



```
virtual : 자식클래스에서 메소드를 재 정의 하고싶을 때 재정의될 부모의 클래스에 매소드에 사용
override : 부모클래스에서 virtual로 선언된 메소드를 재정의 할 때 사용
```



```c#
using System;

namespace ConsoleApplication21
{
	class Parent
	{
		public virtual void A() // 자식클래스에서 재정의 되게 설정함
		{
			Console.WriteLine("부모 클래스의 A() 메서드 호출!");
		}
	}
	class Child : Parent
	{
		public override void A() // virtual으로 재정의된 메서드를 재사용
		{
			Console.WriteLine("자식 클래스(Child)의 A() 메서드 호출!");
		}
	}
	class Daughter : Parent
	{
		public override void A()
		{
			Console.WriteLine("자식 클래스(Daughter)의 A() 메서드 호출!");
		}
	}
	class Program
	{
		static void Main(string[] args)
		{
			Parent parent = new Parent();
			parent.A();
			
			Child child = new Child();
			child.A();
			
			Daughter daughter = new Daughter();
			daughter.A();
		}
	}
}
```



결과 : 

```
부모 클래스의 A() 메서드 호출!

자식 클래스(Child)의 A() 메서드 호출!

자식 클래스(Daughter)의 A() 메서드 호출!

계속하려면 아무 키나 누르십시오 . . .
```



*매소드를 재정의 하려면 virtual 키워드가 **꼭** 붙어있어야한다.  

  그렇지 않으면 다음과 같은 오류가 발생한다.



*또한 private로 접근 범위가 제한된 메서드는 재정의 할 수 없습니다.

```
오류	1	'ConsoleApplication21.Child.A()': 상속된 'ConsoleApplication21.Parent.A()' 멤버는 virtual, abstract 또는 override로 표시되지 않았으므로 재정의할 수 없습니다.	C:\Users\h4ckfory0u\documents\visual studio 2012\Projects\ConsoleApplication21\ConsoleApplication21\Program.cs	18	30	ConsoleApplication21

[재정의될 메서드가 virtual로 표시되지 않으면 재정의를 할 수 없다는 에러]
```

  

**멤버 숨기기(new)**

---



new 지정자를 사용하면 부모 클래스의 멤버를 숨길 수 있게됩니다.  



*부모와 자식의 메서드 이름이 같을 때 쓴다

```c#
using System;
namespace ConsoleApplication21
{
	class Parent
	{
		public int x = 100;
		public void A()
		{
		Console.WriteLine("부모 클래스의 A() 메서드 호출!");
		}
	}
	
	class Child : Parent
	{
		public new int x = 200;  // [부모의 메서드와 자식의 메서드의 이름이 같다]
		public new void A() // 이경우에는 new로 멤버를 숨겨주지 않아도 상관 X
		{
		Console.WriteLine("자식 클래스(Child)의 A() 메서드 호출!");
		}
	}
	
	class Program
	{
		static void Main(string[] args)
		{
			Parent parent = new Parent();
			parent.A();
			Console.WriteLine("x : {0}", parent.x);
			
			Child child = new Child();
			child.A();
			Console.WriteLine("x : {0}", child.x);
		}
	}
}
```



```
부모 클래스의 A() 메서드 호출!
x : 100

자식 클래스(Child)의 A() 메서드 호출!
x : 200

계속하려면 아무 키나 누르십시오 . . .
```



**업캐스팅과 다운캐스팅(Upcasting and Downcasting)**

---



업캐스팅과 다운캐스팅은 객체 지향 프로그래밍의 특징 중 하나인 **다형성(polymorphism)**과 밀접한 관련이 있다.    



```c
[다형성(polymorphism)은 무엇인가요?]



polymorphism에서 poly는 여러, 다양한(many), morph는 변형(change)이나 형태(form)의 의미를 가지고 있습니다. 사전적 정의로만 살펴보면 "여러가지 형태"를 나타내는데, 이를 객체 지향 프로그래밍으로 끌고 온다면 "하나의 객체가 여러 개의 형태를 가질 수 있는 능력"이라 말할 수 있습니다. 



ex) 메소드의 오버로딩 과 오버라이딩
```



[Upcasting]  

자식클래스의 객체 ▶ 부모클래스의 형태로 변환    



[Downcasting]  

부모클래스의 객체 ▶ 자식클래스의 형태로 변환    



```c#
class Animal { }

class Dog : Animal { }

Dog dog = new Dog();//이 객체를 빼주면 다운캐스팅에서 오류발생
Animal animal = dog; // 업캐스팅
Dog sameDog = (Dog)animal; // 다운캐스팅, Dog클래스의 객체이기때문에 오류 발생 X
```



다음과 같이 Dog클래스와 Animal클래스로 예를 들자면, 

개(Dog)는 동물 (Animal)의 상태를 모두 가지고있으므로 변환 O    



But,    



Animal 클래스의 객체를 Dog 클래스의 형태로 바꾸려 하면 문제가 발생한다.

동물 (Animal)는 개(Dog) 의 고유한 상태를 가지고있지 않으므로 변환 X    



---



[출처] : https://blog.hexabrain.net/142
