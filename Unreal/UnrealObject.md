---
 layout: post
 title: Unreal-Engine-Day3
 date: 2021-02-06 4:10:47 +07:00
 tags: [Unreal, game]
---

#### 오늘할것

````
1.새 프로젝트 파일에 방만들기
2.공간 비우는 법 알고 문 만들기
````



#### 기본적인 용어 설명

---

■ Level : 일반 게임들(보글보글, 궁수의 전설같은 게임들) 에 나오는 게임 한판 한판 <br>
■ Actor : 레벨을 제일처음 생성했을때 있는 모든 구성요소<br>
■ RGB : 지오메트리를 생성했을때 나타나는 화살표 각축의 크기를 가지고있음(R = X , G = Y , B = Z)



#### 지오메트리 생성하기
---

![img](https://cdn.discordapp.com/attachments/804184517644386345/807596183621992498/unknown.png)

옆 모드창에서 지오메트리칸에 도형을 레벨창에 드래그해서 가져올 수있습니다.



#### Tips.

---

![img](https://cdn.discordapp.com/attachments/804184517644386345/807596620778045510/unknown.png)

```
가져온 도형을 Brush Settings의 x,y,z값을 조정해 스케일을 조정할 수있습니다.
Tip. 언리얼에서는 모든 길이의 단위가 [cm]입니다.
```

![img](https://cdn.discordapp.com/attachments/804184517644386345/807597691969732618/unknown.png)

![img](https://cdn.discordapp.com/attachments/804184517644386345/807598549599911956/unknown.png)

```
다음 버튼을 누르면 오브젝트를 회전 시킬 수 있습니다.
```

---



#### 방 만들어주기

---



다음과같은 방을 만들어 주었습니다!

![img](https://cdn.discordapp.com/attachments/804184517644386345/807598288165142558/unknown.png)

![image-20210206220910348](C:\Users\User\AppData\Roaming\Typora\typora-user-images\image-20210206220910348.png)

다음과 같이 나가지못하니 문을 뚫어 주어야 겠습니다. <br>

■옆의 지오메트리에서 박스를 하나 꺼냅니다.

![img](https://cdn.discordapp.com/attachments/804184517644386345/807596183621992498/unknown.png)

■Brush Settings칸에서 Brush Type를 Subtractive로 바꾸어줍니다

![img](https://cdn.discordapp.com/attachments/804184517644386345/807599420303474708/unknown.png)

■ 다음과같이 구멍이 생긴것을 알 수있습니다

![img](https://cdn.discordapp.com/attachments/804184517644386345/807600177225531402/unknown.png)

■ 방금의 빈공간을 이용해서 문도 만들어 주었습니다!

![img](https://cdn.discordapp.com/attachments/804184517644386345/807600131788242944/unknown.png)

---
