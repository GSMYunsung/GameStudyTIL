#### Vector

백터는 `좌표`와 `방향`을 나타낸다.

유니티에서는 `Vector2,Vector3,Vector4` 사용

4는 쉐이더를 설정 할때 쓰인다.

```
2 : x,y좌표

3 : x,y,z좌표
```

유니티에서 왼손좌표계를 쓰기때문에 z 앞쪽 즉 forward값이다.

![img](https://cdn.discordapp.com/attachments/735007340733923392/808631631987474452/unknown.png)

> ​    [유니티 좌표]               [유니티 코드]
>
> new Vector3(1,1,1)  ==    Vector3.one
>
> new Vector3(0,0,-1)  ==    Vector3.back
>
> new Vector3(0,-1,0)  ==    Vector3.down
>
> new Vector3(0,0,1)  ==    Vector3.forward
>
> new Vector3(-1,0,0)  ==    Vector3.left 
>
> new Vector3(1,0,0)  ==    Vector3.right 
>
> new Vector3(0,1,0)  ==    Vector3.up 
>
> new Vector3(0,0,0)  ==    Vector3.zero



##### **벡터 연산**

위의 Static으로 정의된 값 이외의 값이 필요하다면, 연산으로 만들 수 있다. 

> ex) (0,8.7,0) 이란 값이 필요하다면 Vector3.up ***** 8.7
>
> ex) (-1,-1,0) 이란 값이 필요하다면 Vector3.left **+** Vector3.down

하지만 Vector3.zero***** Vector3.down 즉, 두 벡터를 곱한다고 해서  (0,0,0) 이 나오진 않음.

**Why?**

`벡터끼리 [곱셈]과 [나눗셈]을 할 수 없기 때문이다.`



##### **Vector Magnitude(크기)**

벡터는 아까도 말했다 싶이 `길이(크기)`도 반환해 준다.

![img](https://cdn.discordapp.com/attachments/735007340733923392/808637503124275220/unknown.png)

벡터의 크기는 `피타고라스의 정리`로 확인할 수있음.

![img](https://cdn.discordapp.com/attachments/735007340733923392/808638940944924702/unknown.png)



**두 좌표의 거리 구하기**



##### **a좌표와 b좌표간의 거리 구하기**

 a 에서 b를 빼 c를 구한 후(c = a - b)  c의 `Magnitude 값`을 얻는다. 

`이 과정을 한방에 해주는 것 Vector3.Distance(a,b)`



`[Vector3.Distance(a,b)가 거리를 얻는 과정]`

1. 파라미터로 받은 두 좌표를 뺄셈하여 결과 벡터를 얻음

2. Magnitude 값을 반환한다.

![img](https://cdn.discordapp.com/attachments/735007340733923392/808640267128930304/unknown.png)

결과적으로 Distance는 `Magnitude를 포함`하므로 루트 연산을한다. 

**But,**

루트 연산은 CPU 부담이 된다.

 작은 양의 괜찮겠지만 많아질 수록 부담은 크게 늘어난다. 

ex) 

캐릭터는 수많은 적들 중 가장 가까운 상대에게 공격을 가한다고 할 때,

수 많은 적들 중 누가 가장 가까운지를 먼저 계산해야 한다. 

캐릭터와 적간의 거리를 구하기 위해 Magnitude를 사용한다고 하면, 

```
[적들이 10마리] : 매 프래임마다 Magnitude 연산 즉, 루트연산을 20번해야 한다. 

[적들이 100마리] : 매 프래임마다 200번의 루트 연산을 해야한다.
```



##### **Add.**

**[루트 연산을 하지 않고 거리를 비교하기]**

`단순히 두 오브젝트 간 거리를 비교 : [sqrMagnitude]`

 sqrMagnitude는 `루트 연산을 하지 않은채` 값을 반환한다. 

```
 ex) 루트(3² + 2²) 에서 [루트 연산만 제거]하여 3² + 2² 값만 반환 한다. 
 즉, 제곱의 덧셈만 판단한다는 소리.
```

반환한 값이 거리를 의미하지 않지만 방향은 표현할 수 있고 루트만 씌운다면 거리가 된다. 

즉 ,  sqrMagnitude 값이 크다는 것은 거리가 멀다는 것이다. 

