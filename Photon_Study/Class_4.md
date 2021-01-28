---
 layout: post
 title: Unity_Photon강의_Day4
 date: 2021-01-25 8:14:47 +07:00
 tags: [UNITY, GAME, MULTIGAME,Photon]
---

#### [RaiseEvent]

---

```c#
void SendEvent()
{
    object[] content = new object[] {new Vector3(10.0f, 2.0f, 5.0f), 1, 2, 5, 10 } ;
    PhotonNetwork.RaiseEvent(0, content, RaiseEventOptions.Default, SendOptions.SendUnreliable); // Content부분에 ViewID를 넣으면 특정 뷰만 판단
}
```

![img](https://cdn.discordapp.com/attachments/735007340733923392/803224174977613824/unknown.png)



#### [이벤트 씬에 배치된 오브젝트 이벤트 받기]

---

```c#
IonEventCallback -> 상속해줌 

public class NetworkManager : MonoBehaviourPunCallbacks, IOnEventCallback
{
         public void OnEvent(EventData photonEvent) // photonEvent로 구분가능,만약 view id 를 보냈다면 view id로 조건을 걸 수도있음
            {
                  if(photonEvent.Code == 0)
                         {
                            object[] data = (object[])photonEvent.CustomData;//받아온 데이터를 읽을 수 있게 풀어준다
                             for (int i =0; i < data.Length; i++) print(data[i]);//사용자가 볼 수 있도록 출력해준다.
                          }
             }
}
```

```c#
public void OnEvent(EventData photonEvent) 
```

■ photonEvent로 구분가능, 만약 view id 를 보냈다면 view id로 조건을 걸 수도있음

```c#
object[] data = (object[])photonEvent.CustomData;
 for (int i =0; i < data.Length; i++) print(data[i]);
```

 ■ 받아온 데이터를 읽을 수 있게 풀어주고 사용자가 볼 수있도록 문자열을 출력한다.



#### [이벤트 받기 [동적오브젝트]]

---

```c#
public class PlayerScript : MonoBehaviourPun
{
    void OnEnable()
       {
            PhotonNetwork.NetworkingClient.EventReceived += EventReceive; // 포톤네트워크(이벤트리스너)를 생성
        }

    void OnDisable()
       {
            PhotonNetwork.NetworkingClient.EventReceived -= EventReceive; // 포톤네트워크(이벤트리스너)를 파괴
        }

    void EventReceive(EventData photonEvent)
       {
            if(photonEvent.Code == 0)
                 {
                    object[] data = (object[])photonEvent.CustomData; 
                    //받아온 데이터를 읽을 수 있게 풀어준다
	        for (int i =0; i<data.Length; i++) print(data[i]); 
                    //사용자가 볼 수 있도록 출력해준다.
                 }
       }
}

```

##### 주의해야할점 

■활성화시 추가, 비활성화시 제거필요
■이벤트 남발하면 안됨
■이벤트 리시버가 들어간 모든 오브젝트를 실행하기때문에 남발하면 느려질 수도있음
■RPC와는 다르게 포톤뷰 컴포넌트를 안거쳐도 아무데나 보낼 수 있음

■ Event listener가 필수로 필요하다. 이벤트를 받을 부분을 담당 (Event listener를 생성,파괴해야하는이유)



#### [변수동기화]

---

##### [OnPhotonSerialize View]-  방에 있을 때 변수 동기화

씬에 배치된 오브젝트는 IPunObservable 인터페이스 구현후
PhotonView의 `Observed Components컴포넌트에 스크립트 대입`

<img src="https://cdn.discordapp.com/attachments/735007340733923392/803185658411745281/unknown.png" alt="img" style="zoom:150%;" />

```c#
public class NetworkManager : MonoBehaviourPunCallbacks, IPunObservable
{
    public string value1, value2;
    
    public void OnPhotonserializeView(PhotonStream stream, PhotonMessageInfo info)
       {
           if (stream.IsWriting) // 마스터 클라이언트인 경우에만 보낸다.
               {
                   stream.SendNext(value1);
	       stream.SendNext(value2);
                }
           else
                {
                   value1 = (string)stream.ReceiveNext();
                   value2 = (string)stream.ReceiveNext();
                 }
          }
}
```
Stream.IsWriting은 `마스터 클라이언트인 경우` 보낸다. `[Send]`
다른 클라이언트들은 보냈던 순서대로 값을 받는다.  `[Get]`

즉,

마스터 클라이언트 : 순서대로 보낸다.
다른클라이언트 : 보냈던 순서대로 받는다. `받기만 가능`

이라는 것이다.



다른 예를 살펴보자.

```c#
if(Stream.IsWriting)
        {
	 stream.SendNext(transform.position);
 	 stream.SendNext(transform.rotation);
         }
else
        {
           curPos = (Vector3)stream.ReceiveNext();
           curRot = (Quaternion)stream.ReceiveNext();
         }
}
```

Stream.IsWriting은 `PV.IsMine이 ture`인 경우 보낸다.
`위치와 회전`을 보낸다.

`PV.IsMine이 false`인 모든 동적 오브젝트는
`보냈던 순서대로 값을 받는다.  받기만 가능하다`



#### [정리]

---

![img](https://cdn.discordapp.com/attachments/735007340733923392/803223630825259008/unknown.png)

##### ++ OnPhotonSeialize View - 변수의 값이 자주바뀌거나 변수의 값이 중요할때 사용하면 좋다



##### Resources

-[Photon멀티게임강의](https://www.youtube.com/watch?v=7tjez6oZDlA)
