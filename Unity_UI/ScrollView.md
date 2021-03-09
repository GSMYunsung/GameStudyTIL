## UI_ScrollView

>게임에서 UI 창보다 크거나 많은 내용이 들어가는 콘텐츠를 UI안에 담기위해 사용하는 UI  



```
[대표적인 방법 두가지]

1.대표적인 방법이 바로 버튼 같은 것을 이용해서 페이지를 넘기는 것
	ㄴ콘텐츠가 연속적이지 않고 흐름이 끊어져도 무관!
	
2.나는 스크롤을 이용해 UI 내에서 이동하면서 볼 수 있는 스크롤 뷰
	ㄴ들어가는 콘텐츠가 하나의것이나 흐름이 연속적!
```



### ScrollView 기본구성요소_

![img](https://cdn.discordapp.com/attachments/804184517644386345/818757240202461184/unknown.png)  



```
1. Scroll View ▶ 우리가 생성한 스크롤 뷰
2.  2.Viewport ▶ 표시하고자 하는 콘텐츠가 보여질 곳
3. Content ▶ 표시하고자 하는 내용물
4. Scrollbar Horizontal ▶ 수평 스크롤바
5. Scrollbar Vertical ▶ 수직 스크롤바
```

![img](https://cdn.discordapp.com/attachments/804184517644386345/818760330342826004/unknown.png)



### Scroll View 기본구성요소

![img](https://cdn.discordapp.com/attachments/804184517644386345/818758229312012308/unknown.png)



```
Horizontal ▶ 스크롤 뷰의 수평 이동을 허용할 것인가?

Vertical ▶ 스크롤 뷰의 수직 이동을 허용할 것인가?

Movement Type ▶ 스크롤 이동 타입 (콘텐츠가 스크롤의 밖,안 등에 있도록)

		- Unrestricted ▶ 콘텐츠가 스크롤 밖으로 나가도록 조금도 제한하지 않는다.

		- Elastic ▶ 콘텐츠가 스크롤 밖으로 나가면 정해놓은 값(Elasticity)만큼의 속도						 로 스크롤뷰 안으로 돌아온다.

		- Clamped ▶ 콘텐츠가 스크롤 밖으로 나가지 못하게 완전히 제한한다.

Inertia ▶ [관성] 이 값을 켜두면 스크롤을 끌다가 놓으면 바로 정지하지 않고 끌던 속도가 점점 

				감소하며 멈춘다.

Scroll Sensitivity ▶ 스크롤 민감도(빠르기)

Horizontal Scrollbar ▶ 수평 스크롤바

Visibility ▶ 스크롤바가 보이는 방식

- 항상 보이는 방식인지 콘텐츠의 크기에 따라 보이는 방식인지를 설정할 수 있다.

  수직 스크롤바 역시 같은 내용이다.
```



+Thinking_🚀

```
UI에서 보여주고자 하는 내용은 모두 Content 오브젝트의 자식으로 배치해야 한다.

 Content의 크기에 따라 스크롤 뷰의 크기가 결정된다(상속)
```



### 스크롤 뷰 크기 조절하기

>아이템 갯수와 같은 요소를 통해서 보여지는 크기가 달라지는 경우 필요

```c#
using UnityEngine;
using UnityEngine.UI;   // UI와 관련된 스크립트 작업을 위해서 추가해 주어야 한다.
using System.Collections;

public class ScrollViewPractice : MonoBehaviour
{
    // 스크롤 뷰와 관련된 수정을 하기 위해 가지고 있는 변수
    ScrollRect scrollRect;

    // Use this for initialization
    void Start ()
    {
        scrollRect = GetComponent<ScrollRect>();    
        // 게임 오브젝트가 가지고 있는 ScrollRect를 가져온다.

    }
   
    void SetContentSize()
    {
        float width = 100.0f;
        float height = 100.0f;
        // scrollRect.content를 통해서 Hierachy 뷰에서 봤던 Viewport 밑의 Content 게임 오브젝트에 접근할 수 있다.
        // 그리고 sizeDelta 값을 통해서 Content의 높이와 넓이를 수정할 수 있다.
        scrollRect.content.sizeDelta = new Vector2(width, height);
    }
}
```


