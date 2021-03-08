---
 layout: post
 title: Unreal_Engine_Day1
 date: 2021-01-22 9:13:47 +07:00
 tags: [UnrealEngine, game]
---

#### [Unreal기초]

---

##### [언리얼 c++개발과 블루프린트 차이점]

언리얼에는 c++로 개발자가 `직접 코드를 작성해서 개발`하는 방법이고, 

블루프린트는 눈에 보이는 노드와 노드를 이어 `기능의 흐름을 눈으로 보고 개발`하는 방법이다.

![img](https://cdn.discordapp.com/attachments/804184517644386345/804185094029049866/unknown.png)



#### [언리얼엔진에서 C++스크립트 생성하기]

---

다음과 같은 에픽게임즈 앱에서 언리얼 엔진을 실행합니다.

![img](https://cdn.discordapp.com/attachments/804184517644386345/804185359964700692/unknown.png)

그리고 새프로젝트>탬플릿 선택[기본]>프로젝트 세팅 프로젝트타입[블루프린트->c++로 바꿈]

(여러가지 설정이 있지만 다음에 알아보도록하자)

그리고 프로젝트를 생성하면 다음과 같은 화면이 나올것이다.

![img](https://cdn.discordapp.com/attachments/804184517644386345/804193386872569856/unknown.png)

이제 c++스크립트를 추가해보자.

여기서 버전에따라 c++스크립트를 추가하는 방법이 달라진다.



#### [4.26버전 이전]

---

콘텐츠 브라우저창에 우클릭후 c++클래스 생성 > 부모클래스 Actor로 변경> 클래스 생성

![img](https://cdn.discordapp.com/attachments/804184517644386345/804188440996085791/unknown.png)

<img src="https://cdn.discordapp.com/attachments/804184517644386345/804187640575819806/unknown.png" alt="img" style="zoom:150%;" />



#### [4.26버전 이후]

---

파일 > 새로운 c++클래스 생성 > 부모클래스 Actor로 변경 > 클래스 생성

![img](https://cdn.discordapp.com/attachments/804184517644386345/804186935412129802/unknown.png)

<img src="https://cdn.discordapp.com/attachments/804184517644386345/804187640575819806/unknown.png" alt="img" style="zoom:150%;" />



#### [생성된 c++코드 설명]

---

```c++
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "MyActor.generated.h"

UCLASS()
class MYPROJECT_API AMyActor : public AActor
{
	GENERATED_BODY() // 헤더파일
	
public:	
	// Sets default values for this actor's properties
	AMyActor();//AMyActor클레스가 생성될때 생성된 변수의 기본값을 설정하는 함수

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override; //엑터가 배치된 월드에서 게임이 시작되거나 엑터가 월드에 스폰되었을때 호출되는 함수, 게임플레이 로직 초기화
									   //유니티의 Start 함수와 동일

public:	
	// Called every frame
	virtual void Tick(float DeltaTime) override; //Tick함수가 호출된 이후 얼마의 시간이 경과했는지 알 수있는 함수, 유니티의 Update함수와 동일
	                                            
   //프로젝트에서 굳이 Tick함수가 필요하지 않다면 Tick함수를 비활성화한후 헤더파일에있는 Tick함수와 PrimaryActorTick.bCanEverTick = true; 코드까지 비활성화
};

```

---

```c++
// Fill out your copyright notice in the Description page of Project Settings.


#include "MyActor.h"

// Sets default values
AMyActor::AMyActor()
{
 	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = true;
	UE_LOG(LogTemp, Log, TEXT("Constructor"));
	//언리얼에서의 문자 출력, UE_LOG(LogTemp, Log, TEXT(""));
	//[언리얼에서 코드변경사항] 
	//1. 저장은 프로젝트 이름 우클릭후 빌드
	//2. 언리얼에 들어간후 컴파일 버튼
}

// Called when the game starts or when spawned
void AMyActor::BeginPlay()
{
	Super::BeginPlay();
	UE_LOG(LogTemp, Log, TEXT("BeginPlay"));
}

// Called every frame
void AMyActor::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);
	UE_LOG(LogTemp, Log, TEXT("Tick"));
}
```

#### [언리얼에서 컴파일하는 방법]

1. 저장은 프로젝트 이름 우클릭후 빌드
2. ![img](https://cdn.discordapp.com/attachments/804184517644386345/804190146417262612/unknown.png)
3. 언리얼에 들어간후 컴파일 버튼

![img](https://cdn.discordapp.com/attachments/804184517644386345/804190327400693760/unknown.png)

그후 게임에 스크립트를 드래그하고 실행하면

![img](https://cdn.discordapp.com/attachments/804184517644386345/804190749742596156/unknown.png)

다음과같은 로그가 나오는데 로그를 살펴보자면,

<img src="https://cdn.discordapp.com/attachments/804184517644386345/804190903094738995/unknown.png" alt="img" style="zoom:150%;" />

게임플레이 로직 초기화가 이루어 졌기때문에 Constructor가 출력

<img src="https://cdn.discordapp.com/attachments/804184517644386345/804190970073448498/unknown.png" alt="img" style="zoom:200%;" />

BeginPlay함수가 실행되어 BeginPlay가 찍힌것을 알 수있다.

<img src="https://cdn.discordapp.com/attachments/804184517644386345/804191046388023306/unknown.png" alt="img" style="zoom:150%;" />

다음으로는 매회 틱함수가 실행되어 Tick함수가 쭉 나열되있는 모습을 볼 수있다.
