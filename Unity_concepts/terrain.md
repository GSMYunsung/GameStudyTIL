#### Terrain 지형



**쓰는이유?**

---



```
유니티에서 지형을 간단한 브러쉬 툴로 만들수있다 .

 작업시간 단축 
 고 퀄리티
 LOD 자동 지원
 Asset Store 를 통한 다양한 지형물 제공
```



**1.지형생성**

----



![img](https://cdn.discordapp.com/attachments/735007340733923392/811834714485948446/unknown.png)

다음과같이 Hierarchy창에서 우클릭 > 3D오브젝트 > Terrain 으로 New Terrain을 생성한다.



* 지형옵션

  ![img](https://cdn.discordapp.com/attachments/804184517644386345/811836652372754462/unknown.png)

    1. 새 지형추가 - 새로운 지형을 추가함
    2. 높이지정,높이조절,스무드,텍스처를 등록 , 색칠 -
       브러쉬로 지형높낮이나 지정높이만큼 지형을 변환후 부드럽게 다듬는기능, 택스처 입히는 기능
     3. 나무    - 브러쉬로 나무 심기
     4. 디테일   - 풀과 돌같은 지형지물 등록후 사용
     5. 환경 설정 - 지형의 환경설정**



**2.지형조절하기**

---



브러쉬 툴로 지형을 조절한다.

![img](https://cdn.discordapp.com/attachments/804184517644386345/811841987338698812/unknown.png)



**3.지형텍스쳐 입히기**

---



![img](https://cdn.discordapp.com/attachments/804184517644386345/811840912304898069/unknown.png)



ㄴ 텍스쳐 브러쉬 옵션중 Target Strength 옵션을 0~1 사이로 두면 새로운 텍스쳐와 기존텍스쳐의 혼합비율을 결정할수있다.

ㄴ Opacity 랑 헷갈릴수 있는데 Opacity 를 낮춘다고 해서 투명X `지형 자체가 흐리게 덮어진다.`- 즉 채도만 낮아진다.

**ㄴ 지형은 보통 15x15사이즈가 적당하다. 값이크면 선명해지나 , 과할경우 깨지는 현상이 발생한다!!**



**4.나무 심기**

---



![img](https://cdn.discordapp.com/attachments/804184517644386345/811843641650708520/unknown.png)

**1. 나무 브러쉬 선택**

**2. Edit Trees -> Add Tree 선택**

**3. 동그라미 선택**

**4. 에셋목록에서 나무 선택 ( 이때 당연히 사용할 에셋을 임포트 한후여야 한다 )** 

**- 왼쪽 버튼으로 브러쉬를 칠하면 나무가 생성되고 , Shift 키를 누르고 하면 나무 제거!!** 



 *** Bend Factor : 나무가 바람에 휘날리는 강도**



![img](https://cdn.discordapp.com/attachments/804184517644386345/811843883259396116/unknown.png)



[랜덤하게 나무의 숫자를 설정하고 싶다면?]

 Edit Trees 왼쪽의 Mass Place Trees 버튼으로 터레인에 랜덤한 숫자의 나무를 랜덤으로 배치 가능!



[예시이미지]

![img](https://cdn.discordapp.com/attachments/804184517644386345/811844219425128468/unknown.png)



**5 . 풀과 바위 심기**

---



○ 디테일 브러쉬 항목으론 풀과 바위를 심을수 있는데 

​	풀은 항상 카메라를 보는 `2D 이미지 방식(빌보드)`을, 

​	바위는 `3D 메쉬`를 이용한다.



**= 풀 그리기**

​	나무와 엇비슷하다

![img](https://mblogthumb-phinf.pstatic.net/20131114_110/winterwolfs_1384412889299bm4UL_JPEG/10.jpg?type=w2)

 

 

**1. 디테일 브러쉬 선택**

**2. Edit Details -> Add Grass 선택**

**3. 동그라미 선택**

**4. 에셋목록에서 풀 선택 ( 자세한 설정을 보면 , Grass 폴더에 있고 2D 텍스쳐인것을 확인할수있다. )**

**- 풀 역시 Shift 키를 누르면 지울수 있다.** 

﻿ 



*** 세부 옵션** 

| . Min Width     | - 풀의 최소 너비                               |
| --------------- | ---------------------------------------------- |
| . Max Width     | - 풀의 최대 너비                               |
| . Min Height    | - 풀의 최소 높이                               |
| . Max Height    | - 풀의 최대 높이                               |
| . Noise Spread  | - 건강한풀의 영역 설정 . 영역 밖은 마른풀이 됨 |
| . Healthy Color | - 건강한 풀 색상                               |
| . Dry Color     | - 마른풀 색상                                  |
| . Billboard     | - 빌보드 on/off                                |

 

**[만일 그린 풀이나 바위가 보이지 않을때]** 

 LOD 기능 ( Level of Detail ) 때문에 `거리에 따른 필터링`이 된것이라 생각하고

 카메라를 가까이 당기면 이쁜 풀이 보일것이다!

 

 

 

**= 바위 그리기**

 바위는 `풀과 거의 같은 방식`이며 , **Edit Details -> Add Details Mesh** 를 선택하면된다.

 

. 선택후 화면

![img](https://mblogthumb-phinf.pstatic.net/20131114_203/winterwolfs_13844139428133YWkf_JPEG/12.jpg?type=w2)

 

**- 옵션 설정**

| . Noise Spread  | - 노이즈 영역의 크기                                         |
| --------------- | ------------------------------------------------------------ |
| . Healthy Color | - 노이즈 영역의 안쪽에 물체 색상                             |
| . Dry Color     | - 노이즈 영역의 바깥족 물체 색상                             |
| . Render Mode   | - 렌더링 모드VertexList = 바위같은 우둘투둘한 물체Grass Lighting = 단순한 물체 |



**하이트 맵 파일 -> RAW 라는 확장자로 저장됨**

하이트 맵 파일은 16비트 8비트 두가지 방식의 저장방법이 있으므로 알고써야함 .



[출처]

---



https://m.blog.naver.com/PostView.nhn?blogId=winterwolfs&logNo=10179874455&proxyReferer=https:%2F%2Fwww.google.com%2F
