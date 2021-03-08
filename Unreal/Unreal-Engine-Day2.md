---
 layout: post
 title: Unreal_Engine_Day2_변수와_UPROPERTY
 date: 2021-01-28 4:21:47 +07:00
 tags: [UnrealEngine, game]
---

#### [변수지정]

----

■프로그래밍의 변수 = 게임에서 사용될 기본적인 값을 담을 수 있는것

    UPROPERTY( ) - 이런 값이있다고 알리는것과 어떻게 동작되는지 설정해줌


#### [변수설정]

----

> UPROPERTY( )

> 헤더파일에서 변수명 변수이름 ;

<img src="https://cdn.discordapp.com/attachments/804184517644386345/804251107580837888/unknown.png" alt="img" style="zoom:150%;" />

#### [변수종류]

----

```c++
//short s; 이런 변수들은 플렛폼에따라 값이 달라짐
//int i;
//long l;


 //비트수가 한단계씩 올라갈때마다 차지하는 매모리수가 더 높아진다.

 //숫자 뒤에 붙은것들은 비트를 사용하는 수

int8 i8; // 127~-128사이 수를 표현 할 수있음.
		 
int16 i16;// 32,767~ -32,768 사이 수를 표현 할 수있음.
int32 i32;// 214ㅡ648ㅡ647 ~ -214,648,648 사이 수를 표현 할 수있음.
int64 i64; //엄청큰수

uint8 ui8;//uint는 음수에 쓸 범위를 가져와 정수에 쓴다. 그만큼 수가 늘어남.
uint16 ui16;
uint32 ui32;
uint64 ui64;

float f;
double d;

FString str; // 문자형

bool b; //참,거짓
```


#### [UPROPERTY지정자 종류]

---

```c++
UPROPERTY(EditAnywhere, BlueprintReadWrite, Category="Damage")          
// EditAnywhere : 블루프린트나 인스팩터 창에서 수정이 가능하게 만들어줌
     int32 TotalDamage;													   
     // BlueprintReadWrite : 블루프린터에서 읽기와 쓰기가 가능하게 만들어                    //Category : 이것을 Damage라는 카테고리로 묶어서 보여주게 만들어줌

	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Damage")
	float DamageTimeInSeconds;

	UPROPERTY(BlueprintReadOnly,VisibleAnywhere, Transient, Category = "Damage") // BlueprintReadOnly : 블루프린트에서는 읽기만 가능하게 해줌
																			     // VisibleAnywhere : 프로퍼티 창에서 볼수만 있게해줌							         // Transient : 해당 프로퍼티가 휘발성이 아니게해줌 즉, 
  //              한번값을 지정하면 프로젝트가 꺼져도 값을 저장하고있음
	float DamagePerSecond;

	UPROPERTY(EditAnywhere, BlueprintReadWrite)
	FString CharacterName;

	UPROPERTY(EditAnywhere, BlueprintReadWrite)
	bool bAttackable;
```



■위와 같이 설정한 함수들이 `Category`로 묶여있고,  `BlueprintReadOnly`로 인해 Damage Per Second가  수정불가능한 프로퍼티가 된것을 알 수있다.

![img](https://cdn.discordapp.com/attachments/804184517644386345/804286187560108032/unknown.png)



#### [변수 초기화]

---

```c++
// Fill out your copyright notice in the Description page of Project Settings.


#include "Sko.h"//소스코드 이름이 SKo

// Sets default values
ASko::ASko() 
	//1.생성자에서 변수 초기화
	: TotalDamage(200), DamageTimeInSeconds(1.0f), CharacterName(TEXT("윤성")), bAttackable(true)
{
	PrimaryActorTick.bCanEverTick = true;
	//2.함수 안에 직접 넣어주기
	TotalDamage = 200;
	DamageTimeInSeconds = 1.0f; 
	CharacterName = TEXT("윤성");
	bAttackable = true;
}

// Called when the game starts or when spawned
void ASko::BeginPlay()
{
	Super::BeginPlay();
	
}

// Called every frame
void ASko::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);

}

```

변수의 초기화는 소스코드에서 할 수있는데, 두가지 방법이 있다. 

> 1.생성자에서 변수 초기화
> : TotalDamage(200), DamageTimeInSeconds(1.0f), CharacterName(TEXT("윤성")), bAttackable(true)

>2.함수 안에 직접 넣어주기
>
>{	TotalDamage = 200;
>	DamageTimeInSeconds = 1.0f; 
>	CharacterName = TEXT("윤성");
>	bAttackable = true; }

자신이 편한대로 골라쓰면 될듯하다.

어쨋든 이렇게 변수를 초기화를 시켜준후 다시 언리얼에 들어가보면

<img src="https://cdn.discordapp.com/attachments/804184517644386345/804284104240922654/unknown.png" alt="img" style="zoom:200%;" />

다음과 같이 변수에 값이 들어간 것을 알 수있다.
