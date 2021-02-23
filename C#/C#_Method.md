#### 메소드



**확장 메소드(Extension Method)**

---

  

> *기존 클래스의 기능을 확장시켜주는 메소드*

  

```c#
[기본형식]

namespace 네임스페이스명
	{
	public static class 클래스명 //정적 클래스 정의
	{
		public static 반환형식 메소드명(this 확장대상형식 식별자, 매개변수..) //확장 메소드 정의
		{ //확장 메소드와 클래스 둘다 [정적 메소드여야 한다], 메소드의 첫번째 매개변수가 this한정자이다
			..
		}
		..
	}
}

//(정적 클래스를 먼저 지정한 후 확장 메소드를 정의함)
```

​    

*ex)*

```c#
using System;
using Extension;
namespace Extension
	{
	public static class ExtensionMethod
	{
		public static int Multiplication(this int var, int a, int b)
		{ //ExtensionMethod클래스의 확장 메소드인 Multiplication으로 각각의 인자를 전달함
			int result = var;
			for (int i = 0; i < b; i++)
			result *= a;
			return result; //연산을 한 후 결과값을 다시 리턴함
		}
	}
}
namespace Example
{
	class Program
	{
		static void Main(string[] args)
		{
		Console.WriteLine("{0}", 5.Multiplication(2, 3));//Multiplication확장 메소드로 들어감
		}
	}
}

```

​     

결과:

```
40

계속하려면 아무 키나 누르십시오 . . .
```

   

   

> 확장 메소드가 사용 되는 경우  

```
이미 빌드된 라이브러리를 참조해서 사용하는중 기존의 클래스를 수정하고싶음 

But, 라이브러리의 소스가 없어서 수정이 불가능
```

즉, 쓰이는 상황은 **코드의 직접적인 수정이 불가능** 하거나,   

클래스가 **sealed로 한정되어 상속을 이용할 수없을때**   

​    

**분할 클래스(Partial Class)**

---



> 클래스를 "분할"하는것



```c#
using System;
namespace Example
{
	partial class Nested
	{
		public void Test() { Console.WriteLine("Test()"); } 
        //partial클래스를 이용해 클래스를 분할
	}
	partial class Nested
		{
		public void Test2() { Console.WriteLine("Test2()"); }
		}
	partial class Nested
		{
	public void Test3() { Console.WriteLine("Test3()"); }
		}
	class Program
	{
		static void Main(string[] args)
		{
			Nested nested = new Nested();
			nested.Test();
			nested.Test2();
			nested.Test3();
		}
	}
}
```



결과:

```
Test()

Test2()

Test3()

계속하려면 아무 키나 누르십시오 . . .
```



> 추가

**컴파일 시** 컴파일러에 의해 하나로 합쳐진다.  

분할에는 **제한이 없고**, 여러 번 분할해도 상관이없다.  

**인터페이스, 구조체**에도 사용가능  

  

**중첩 클래스(Nested Class)**

---



> 클래스 내에 클래스가 정의된 클래스   

   

- 외부에 정의하는것보다 관련있는 클래스를 내부 클래스로 두어 코드를 쉽게 이해하기 위해 사용된다.  
- 확장 메서드가 클래스를 확장해주는거라면 중첩 클래스는 클래스두개를 합치는것이라 생각하면 이해가 쉽다. 

```c#
[기본형식]

class 클래스명
{
	class 클래스명
	{
		..
	}
}
```



*ex)*  

```c#
using System;
namespace ConsoleApplication21
{
	public class OuterClass
	{
		private int a = 70;
		
		public class InnerClass
		{
			OuterClass instance;
		
		public InnerClass(OuterClass a_instance)
		{
			instance = a_instance;
            // instance 객체에 OuterClass의 객체인 a_instance를 가져옵니다

		}
	
		public void AccessVariable(int num)
		{
			this.instance.a = num;
            //매개변수 num을 받아 num 값을 가지고 instance 객체의 멤버 변수 a의 값을 수정
            //안쪽에 정의된 클래스에서 바깥쪽에 정의된 클래스의 private 변수에 접근가능
		}
	
		public void ShowVariable()
		{
			Console.WriteLine("a : {0}", this.instance.a);
		}
	}
}

	class Program
	{
		static void Main(string[] args)
		{
		OuterClass outer = new OuterClass();
		OuterClass.InnerClass inner = new OuterClass.InnerClass(outer);
        //InnerClass의 생성자에 OuterClass의 객체를 넘겨준다.
		inner.ShowVariable();
		inner.AccessVariable(60);
		inner.ShowVariable();
		}
	}
}
```

  

> 추가  

내부에 쓰인 클래스는 제한자가 명시되어있지않으면 private 보호수준이 된다.  



출처:https://blog.hexabrain.net/144?category=442691
