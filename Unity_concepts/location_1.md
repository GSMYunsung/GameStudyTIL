#### 좌표계_1

**좌표계 종류**

---



[2D 좌표계]

`x축과 y`축으로만 이루어져있는 사분면이다. 데카르트 좌표계라고도 한다고한다.

![img](https://cdn.discordapp.com/attachments/735007340733923392/810784704894599208/unknown.png)

[3D 좌표계]

`x축과 y축 z축`으로 이루어져 있는 좌표계이다. 왼손 좌표계 라고도 한다.

![img](https://cdn.discordapp.com/attachments/735007340733923392/810785061808111626/unknown.png)



**로컬 좌표계와 월드 좌표계**

---



[Local좌표]

우리가 Inspector 상에서 보는 Position 값은 *`Local`좌표이다.

즉, transform.position == transform.localPosition이다.

하지만 해당 오브젝트가 루트라면 같겠지만 누군가의 자식이라면 다를 것이다.

(만약 누군가의 자식이라면 부모의 좌표를 따라가기 때문이다.)



```
*Local좌표 : 자신을 기준으로 하는 공간 
```



ex) 내가 컵을 손을 쭉뻗어서 들고있고 이는 내기준으로 ( 1, 0, 0 ) 위치라고하면

​	   여기서 컵을 들고 아무리 달리고 움직여도 컵을 든 손의 위치를 바꾸지 않는 이상은

​       여전히 내 기준으로는 ( 1, 0, 0 ) 이다.  이것이 로컬좌표이다.(월드기준은 컵의 위치가 바뀌어있음)



[World 좌표]

오브젝트의 위치를 나타내는 좌표계로, `화면의 중심을 원점`(0,0,0)으로 하는 3차원 상대좌표계입니다.

```
월드 좌표계는 게임 화면을 투영하는 카메라의 위치와 회전 상태에 따라 달라지므로 반드시 화면의 중심이 원점이 되는것은 아닙니다.
```



**Center / Pivot**

---



Center / Pivot 은 쉽게 말하자면 회전의 기준이다. 

ex) B가 A의 자식이라고 가정할때를 보면 이해가 빠르다.



![img](https://cdn.discordapp.com/attachments/804184517644386345/810790153291300924/unknown.png)

[`Center`를 기준으로 돌릴때]

![img](https://cdn.discordapp.com/attachments/804184517644386345/810790455897620490/unknown.png)

[`Pivot` 을 기준으로 돌릴때]

![img](https://cdn.discordapp.com/attachments/804184517644386345/810790826854318092/unknown.png)

다음과 같이 Center를 기준으로 돈다 가정할때는 자신의 중심점을 이용해 돌지만,

Pivot을 기준으로 돈다 가정하면 부모를 기준으로 돌기때문에 B도형이 아래로 간것을 알 수있다.





**Local / Global**

---



Center / Pivot은 회전을 어떻게 하는지에대한 설정이라면, 

Local / Global은 축을 어떻게 표시하냐에 대한 설정이다.

즉, 물체가 회전을 했을때의 축표현에 대한 설정인것이다.



다음 물체가 회전한다고 해보자.

![img](https://cdn.discordapp.com/attachments/804184517644386345/810792214343057418/unknown.png)

[`Local` 을 기준으로 90도 회전했을때의 축]

![img](https://cdn.discordapp.com/attachments/804184517644386345/810792276392542248/unknown.png)

[`Global` 을 기준으로 90도 회전했을때의 축]

![img](https://cdn.discordapp.com/attachments/804184517644386345/810792318886084608/unknown.png)

정리하자면 `Local`로 두고서 회전을 하게되면 축도 함께 회전하게 되지만,

`Global `로 두고서 회전을 하게되면 축이 월드 좌표계에 고정되어있어 함께 회전하지않고

제자리에 있는다.



**스크린좌표**

---



스크린 좌표계는 단말기의 화면 좌표계로, 화면의 `왼쪽 아래를 원점`으로 하는 평면 절대좌표계입니다.



```
[마우스 클릭이나 터치]는 스크린 좌표계를 이용해서 처리합니다. 
이 좌표계는 카메라의 위치나 각도와 상관없이 일정합니다.
```

<img src="https://cdn.discordapp.com/attachments/804184517644386345/810796813766098964/unknown.png" alt="img" style="zoom:200%;" />



**뷰 포트 좌표**

---



화면에 글자나 2D 이미지를 표시하기 위한 좌표계

화면의 왼쪽 아래를 (0,0) 오른쪽 위를 (1, 1)로 하는 평면 상대 좌표계입니다.

<img src="https://cdn.discordapp.com/attachments/735007340733923392/810798193834328114/unknown.png" alt="img" style="zoom:200%;" />

![img](https://cdn.discordapp.com/attachments/804184517644386345/810797871073984552/unknown.png)

