---
 layout: post
 title: Unity_Photon강의_Day2
 date: 2021-01-22 9:13:47 +07:00
 tags: [unity, game, Multigame,Photon]
---

### <u>[동적오브젝트로 있는경우]-방참가 런타임시</u>

---

(View ID는 고정된다)![img](https://static.wixstatic.com/media/1c4e22_3fd558e2cf8e4de889a91f02b9c1f4d3~mv2.png/v1/fill/w_780,h_309,al_c,lg_1,q_90/1c4e22_3fd558e2cf8e4de889a91f02b9c1f4d3~mv2.webp)

#### Owner - 주인<br>

---

[1] 액터넘버 - 방에 참가한 순서대로 1부터 증가(순서를 나타냄)<br>

※no playername set - 닉네임 설정시 표시



View ID : 1 + 001, 엑터넘버와 엑터넘버가 주인인 포톤 뷰 컴포넌트<br>

​		        [ex.100번째 유저일때 100+001 = 100001]



Controlled locally : 제어권(master)가 붙으면 방장이라는뜻이고,체크와는 별개로<br>

​								  true면 자기자신의 통제권 즉 컨트롤권을 얻음<br>

​                                  (PV.IsMine과 같다)

```c#
public class NetWorkManager : MonoBehaviourPunCallbacks
{
          void Start()
	{
                  Screen.SetResolution(540, 960, false);
 	      PhotonNetwork.ConnectUsingSettings();
             }

           public override void OnConnectedToMaster()
              {
                   PhotonNetwork.JoinOrCreateRoom("Room",new RoomOptions {maxPlayers = 5},none)
              }
           public override void OnJoinedRoom()
	 {
	      PhotonNetwork.Instantiate("Player", Vector3.zero, Quaternion.indentity)
	 }
```

■MonoBehaviourPuncallbacks - 플레이어를오버라이딩 할경우

■MoneBehaviourPun - 플레이어를 굳이 오버라이딩 하지 않을경우

■PhotonNetwork=포톤네트워크의 기본적인 설정들을 지정해준다.

■OnconnectedToMaster은 방의 기본설정을 건드려 방의 이름,플레이어 수등을 결정한다.

■OnjoineRoom = 실제 방에 들어왔을때 플레이어의 이동,회전을 설정해준다


![img](https://static.wixstatic.com/media/1c4e22_6d8aede20326479b914bfefd377a57aa~mv2.png/v1/fill/w_573,h_309,al_c,lg_1,q_90/1c4e22_6d8aede20326479b914bfefd377a57aa~mv2.webp)

■플레이어에 Photon View를 추가해 포톤네트워크에서 인식할 수 있게 설정.

<img src="https://static.wixstatic.com/media/1c4e22_d8994d9f7a6f4559814200126d47cf58~mv2.png/v1/fit/w_293,h_96,al_c,q_5/file.png" alt="img" style="zoom: 200%;" />

■다음과같이 자동으로 IsMine(통제권)과 첫번째 Player라 Master권한이 들어온걸 볼 수있다.

---

##### Resources

-[Photon멀티게임강의](https://www.youtube.com/watch?v=7tjez6oZDlA)
