#### C# 클래스의 상속_1



**[클래스의 개념]**

---



```
객체 지향 프로그램에선 부모 클래스와 자식클래스가 있습니다. 
거기서 [부모 클래스]는 자식 클래스의 기반이 된다하여 기반클래스라고 부르기도하고, 
[자식클래스]는 부모 클래스로부터 파생되었다고 하여 파생 클래스라고 부르기도 합니다.
```



**▶클래스를 다른클래스로 상속하기**

---



```c#
class 부모 클래스
{

}
class 자식 클래스 : 부모 클래스
{
// 부모 클래스의 모든 상태와 행동 전달
}
```



![img](https://cdn.discordapp.com/attachments/804184517644386345/813034490002931712/unknown.png)

부모 클래스를 상속받은 자식클래스는 부모클래스의 모든 맴버를 물려받게 됩니다.

`즉, 다음과 같은 설정들을 모두 받아온다는 소리`

![img](https://cdn.discordapp.com/attachments/804184517644386345/813033973788704838/unknown.png)

단, 생성자는 상속이 되지않고, `생성지 부모 클래스의 생성자가 자동으로 호출`됩니다.

+`private로 선언된 멤버는 상속할 수 없습니다.`



**[예제]**

```
using System;

namespace TestTypeClass
	{
	class Parent
		{
			public int num;
			
			public Parent()
		{
			Console.WriteLine("부모 클래스의 생성자가 호출되었습니다.");
		}
	}
	
	class Child : Parent
	{
		public Child(int num)
		{
			this.num = num;
			Console.WriteLine("자식 클래스의 생성자가 호출되었습니다.");
		}
	public void DisplayValue()
	{
		Console.WriteLine("num의 값은 {0} 입니다.", num);
	}
  }
	class Program
	{
		static void Main(string[] args)
		{
			Child cd = new Child(20);
			cd.DisplayValue();
		}
	}
}
```

결과:

```
부모 클래스의 생성자가 호출되었습니다.

자식 클래스의 생성자가 호출되었습니다.

num의 값은 20 입니다.

계속하려면 아무 키나 누르십시오 . . .
```



[Parent 클래스]

Parent 클래스 내에는 num이라는 멤버 변수와 생성자가 있습니다. 

Parent 클래스를 Child 클래스에 상속시키고 있는 것을 볼 수 있습니다.



[Child 클래스] 

내부를 보시면 생성자와 DisplayValue()라는 메소드가 존재합니다. 

매개변수 하나를 받고, 부모 클래스로부터 물려받은 멤버 변수 num을 

매개변수(int num)의 값으로 초기화시킵니다. 



[DisplayValue 클래스]

num의 값 출력을 하는 클래스입니다.



출력순서를 봐보면 부모 ▶ 자식 ▶ 값출력이다.

따라서 해석을 하자면  `생성자의 호출 순서를 보니 부모 클래스의 생성자가 먼저 호출`되고, 

자식 클래스의 생성자는 그 뒤이어 호출됨을 확인할 수 있습니다.

즉, 부모 클래스의 멤버 변수 num의 값을 출력시킨 것과 같습니다. 



**[자식클래스에서 부모 클래스의 맴버 변수에 접근하기]**

this 키워드를 사용하여 부모 클래스의 멤버 변수에 접근은 할 수 있습니다. 

```
▶자식클래스에도 부모클래스와 같은 변수명이 있다면?

그럴 때는 this 키워드가 아닌 base 키워드를 사용하면 된다.
```

```c#
public Child(int num)
{
base.num = num;
Console.WriteLine("자식 클래스의 생성자가 호출되었습니다.");
}
```



**sealed**

----



클래스 명앞에 sealed 키워드를 사용하게 되면, 해당 클래스를 상속시킬 수 없다.

`즉, 해당클래스가 다른클래스의 부모클래스가 될 수없다.`



```c#
..
	sealed class Parent
		{
			public int num;
			
			public Parent()
		{
			Console.WriteLine("부모 클래스의 생성자가 호출되었습니다.");
		}
	}
	
	class Child : Parent
	{
		public Child(int num)
		{
			this.num = num;
			Console.WriteLine("자식 클래스의 생성자가 호출되었습니다.");
		}
	public void DisplayValue()
	{
		Console.WriteLine("num의 값은 {0} 입니다.", num);
	}
  }
..
```



sealed를 넣고 컴파일을 시도 했더니 다음과 같은 오류가 떳습니다.

```
오류	1	'TestTypeClass.Child': sealed 형식 'TestTypeClass.Parent'에서 파생될 수 없습니다.	c:\users\h4ckfory0u\documents\visual studio 2019\Projects\TestTypeClass\TestTypeClass\Program.cs	19	11	ConsoleApplication8
```



해석하자면 ,  'sealed 형식인 Parent 클래스로부터 파생될 수 없다'라는 에러이다.

sealed 키워드를 사용하면, `의도하지 않은 상속을 불가능`하게 만들 수 있습니다.



**set,get**

---



set, get 접근자는 각각 속성을 읽거나, 새 값을 할당할 때 사용됩니다. 

우리는 때로 객체 지향 프로그래밍에서 **정보 은닉(information hiding)**을 위해 클래스 내부에서만 

사용할 수 있도록 private로 접근을 제한해 버립니다.



```c#
[정보 은닉이란?]

이는 객체 지향 프로그래밍과 밀접한 관련이 있습니다. 클래스 내부의 필드나 메소드와 같이 객체가 가지고 있는 것들을 외부에서 접근하지 못하도록 숨기는 것을 말합니다. 


우리가 클래스를 설계할 때, private나 public 등과 같은 접근 제한자를 통하여 특정 멤버를 공개할 것인지 공개하지 않을 것인지 지정해 줄 수 있었습니다. 

[왜 이러한 작업을 하는 걸까?] 

1.
우리가 클래스를 설계할 때, 수십에서 수백 개에 달하는 필드나 프로퍼티(property)가 존재할 수 있습니다. 그러나 이러한 정보들을 외부로 모두 노출시켜 버리면 우리가 설계한 클래스를 사용하는 사람의 입장에서는 상당히 곤혹스러울 것입니다. 
(이럴 때는 필요한 정보만을 외부로 노출시킬 필요가 있습니다.)

2.
안정성을 위한 것입니다. 객체 내부에서만 사용되는 필드나 메소드는 외부로 공개하면, 
외부에서 이를 수정할 수 있기 때문에 안정성이 깨질 우려가 있기 때문입니다. 

-------------------------------------------------------------------------------
public class Person {
	public String name;
	public int age;
	
	public Person() {
	// ...
	}
	
	// ...
}
-------------------------------------------------------------------------------

위와 같이 Person이란 클래스가 있다면, 외부에서 name과 age를 수정할 수 있습니다.
    
접근 제한자가 public으로 지정되어 있기 때문이다. 하지만 우리는 다른 사용자가 마음만 먹으면 바꿀 수 있는 name이나 age의 값을 신뢰할 수 있을까? 

그렇기 때문에 name과 age 필드의 접근 범위를 private로 제한해줄 필요가 있습니다. 

```



private접근 제한자를 사용하면 외부에서 이 속성을 변경할 수가 없습니다.

하지만 프로그램을 만들다 보면, 내부에 있는 변수를 수정해야 할 상황이 벌어질 수도 있습니다.

 그럴 때 쓰이는 것이 `set, get 접근자`입니다.



```
get 접근자만 존재 : 읽을 수만 있다.

set 접근자만 존재 :  쓸 수만 있다. 

두 접근자가 모두 존재 : 읽을 수도 있고, 쓸 수도 있게 된다.
```



```c#
using System;

namespace ConsoleApplication14
{
	public class MyClass	
	{
		private string name = "John";
		
		public string Name
		{
			get
			{
				return name;
			}
			set
			{
				name = value;
			}
		}
	}
	class Program
	{
		static void Main(string[] args)
		{
		MyClass mc = new MyClass();
		
		Console.WriteLine("mc.Name : {0}", mc.Name);
		
		mc.Name = "Bree";
		
		Console.WriteLine("mc.Name : {0}", mc.Name);
		}
	}
}
```



결과:

```
mc.Name : John

mc.Name : Bree

계속하려면 아무 키나 누르십시오 . . .
```



*name 속성이 private로 접근이 제한되어 있음을 알 수 있다.

 (따라서 name이라는 값에 일반적인 방법으로 접근이 불가능 하다는것을 알 수있다.)



**[Name 이라는 이름의 get, set 접근자]**

 Name이란 이름으로 get/set 접근자를 통해` name에 접근`할 수 있다.



```
get 영역 내에서는 name의 값을 반환하고, 

set 영역 내에서는 name 속성에 value 값으로 초기화!
```



*여기서 value은 Name으로 넘어온 값 즉, "Bree"



27행에서 mc.Name :  John

29행에서 mc.Name : Bree

31행에서 mc.Name을 출력



그리고 get/set 접근자 내에서 value에 변화를 주거나, 주지 않을 수도 있습니다.


---



[출처] : https://blog.hexabrain.net/142

