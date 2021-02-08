#### 1인칭 FPS 카메라 이동

----



```
using System.Collections;
using System.Collections.Generic;
using UniryEngine;

public class CamRotate : MonoBehaviour {

	public float ro_Speed = 200;
	
	void start()
	{
	
	}
	
	void update(){
	float h = Input.GetAxis("Mouse X"); //마우스 X축의 회전을 감지
	float v = Input.GetAxis("Mouse Y"); //마우스 Y축의 회전을 감지
	
	Vector3 dir = new Vector3(v,h,0); // [회전방향] 
										좌우를 바라보는것은 y축이 회전하는것,
										위 아래를 바라보는것은 X축이 회전하는것
	
	transform.eulerAngles += dir * ro_Speed * Time.daltaTime;
    // 카메라의 각도 = 회전방향 * 회전속도 * [시간맞춤?] 
	
	}
}
```

■ 좌우는 문제없이 회전. 

■ `마우스를 위로올리면 아래로, 아래로 내리면 위로 올라가는 문제발생`

■ `위로 올리면 끝까지 올라가는 버그발생`



```
using System.Collections;
using System.Collections.Generic;
using UniryEngine;

public class CamRotate : MonoBehaviour {

	public float ro_Speed = 200;
	
	void start()
	{
	
	}
	
	void update(){
	float h = Input.GetAxis("Mouse X"); //마우스 X축의 회전을 감지
	float v = Input.GetAxis("Mouse Y"); //마우스 Y축의 회전을 감지
	
	Vector3 dir = new Vector3(v,h,0); // [회전방향] 
										좌우를 바라보는것은 y축이 회전하는것,
										위 아래를 바라보는것은 X축이 회전하는것
	Vector3 angle = transform.eulerAngles;
	angle += dir * ro_Speed * Time.daltaTime;
    // 카메라의 각도 = 회전방향 * 회전속도 * [시간맞춤?] 
	
	//위를 바라볼 경우 : 90도 이상이 되면 90도이하로 내려갈때까지 90도로 계속 고정
	//아래를 바라볼 경우 : -90도 이하가 되면 -90도이상으로 내려갈때까지 -90도로 계속 고정
	
	//[각도의 범위] : -90 < 각도 < 90
	
		if(angle >=90){
			angle.x = 90;
		}
		else if (angle <= -90)
		{
			angle.x = -90
		}
	  transform.eulerAngles = angle // 각도 범위 설정후 다시 제한해주기
	}
}
```

#####  [문제]

■ `마우스를 올리거나 내리면 뚝뚝 끊어져 제한되는 현상`

■ `마우스를 위로올리면 아래로, 아래로 내리면 위로 올라가는 문제발생`



##### [`마우스를 위로올리면 아래로, 아래로 내리면 위로 올라가는 문제발생` ]



---

```
스크린의 (0,0)좌표 : 좌 상단에 위치

우리가 생각하는 좌표 : 좌 하단에 위치

x에 -1곱하기
```



##### [`마우스를 올리거나 내리면 뚝뚝 끊어져 제한되는 현상`]



---

```
eulerAngle은 각도가 0 아래, 즉 음수에 위치하게 되면 유니티에서 

자체적으로 360도를 더해 계산을 하게 됨 

eulerAngles의 자동적인 기능이기 때문에 각도의 자체관리가 필요함
```



```
using System.Collections;
using System.Collections.Generic;
using UniryEngine;

public class CamRotate : MonoBehaviour {

	public float ro_Speed = 200;
	//각도의 자체관리
	float mx;//마우스 x각도
	float my;//마우스 y각도
	void start()
	{
	
	}
	
	void update(){
	float h = Input.GetAxis("Mouse X"); //마우스 X축의 회전을 감지
	float v = Input.GetAxis("Mouse Y"); //마우스 Y축의 회전을 감지
	
	mx += h * ro_Speed * Time.deltaTime; //마우스 x축각도 회전
	my += v * ro_Speed * Time.deltaTime; //마우스 y축각도 회전
	
			my = Mathf.Clamp(my, -90, 90); //my의 최대 최솟값을 설정해주어 카메라가 그 이상 
									         회전하지 못하게 만듬
	  transform.eulerAngles = new Vector3(-my, mx, 0);
	  //마우스를 위로올리면 아래로, 아래로 내리면 위로 올라가는 문제
	  //-1을 곱해줘 반대로 x축이 이동하게 해줌
	}
}
```



사실상 이 두개의 코드는 같은역할인 `카메라의 각도 제한  `  기능을 수행해준다.

```
	//위를 바라볼 경우 : 90도 이상이 되면 90도이하로 내려갈때까지 90도로 계속 고정
	//아래를 바라볼 경우 : -90도 이하가 되면 -90도이상으로 내려갈때까지 -90도로 계속 고정
	
	//[각도의 범위] : -90 < 각도 < 90
	
		if(my >=90){
			my = 90; 
		}
		else if (my <= -90)
		{
			my = -90
		}
```

```
my = Mathf.Clamp(my, -90, 90); // 최솟값 최대값 설정후 그 안에서만 값이 설정될 수있도록 해줌
```

---

