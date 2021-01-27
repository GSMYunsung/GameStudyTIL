---
 layout: post
 title: Unity_Photon강의_Day3
 date: 2021-01-22 9:31:47 +07:00
 tags: [unity, game, Multigame, Photon]
---

#### [RPC 채팅]

---

일반함수는 통신이 안되니까 같은 View ID끼리는 <u>같은 함수</u>를 실행하라

##### [같은채널에서 채팅치면 같은채널에있는 사람들끼리 볼 수있는 시스템이라 정리하면됨]

※같은 PlayerScript를 가져도 같은 View ID를 가지고있지않으면 동시에 

실행되도 적용이 되지 않음.

![img](https://static.wixstatic.com/media/1c4e22_1a105c547c3244a0b0da351d758a899d~mv2.png/v1/fill/w_925,h_400,al_c,q_90,usm_0.66_1.00_0.01/1c4e22_1a105c547c3244a0b0da351d758a899d~mv2.webp)

#### [로컬과 리모트(동적 오브젝트)]

---

​	■로컬 = IsMine이 <u>있는것</u>

​	■리모트 = IsMine이 <u>없는것</u>

```c#
public class PlayerScript : MonoBehaviourPun
{
          PhotonView PV; //PhotonView 컴포넌트 받아오기

          void Start()
	{
                  PV = photonView;

 	      if(PV.ISMine) PV.RPC("TestRPC", RpcTarget.All, "A", "B");
             }//PhotonView의 ismine설정의 RPC를 모두에게 실행하라

           void TestRPC(string value1, string value2)
              {
                   print("RPC 실행"); // A,B받아오고 실행
              }
}
```

#### [PhotonView설정]

---

​	■만약 photonView안에 ISMine이 true이면 TestRPC라는 이름의 RPC를 실행  

​       한다.

​	■ RPCTarget의 범위를 모두하고 매게변수를 설정한다. 

​	■모두에게 실행하게 한다.

#### [RPCTarget]

---

​	■All : 자기는 <u>함수바로실행!</u> 그후 다른사람모두에게 전달(자기가 제일빠름)

​        ■AllBuffered : All은 호출하는 시기에 통신하고 사라짐 But!

​	   <u>버퍼에 남겨두면</u> 방에 나갔다 온 사람들에게도 전달됨.

​	■AllBufferedViaServer : 버퍼에 남겨둔 모두에게 서버를 거쳐서<u> 동시호출!</u>

​	    자기와 다른 사람들의 함수 <u>실행 타이밍이 같음</u>

​	■AllViaServer : 모두에게 서버를 거쳐서 <u>동시호출!</u>

​	■MasterClient : 방장한테만 전달

​	■Others : <u>나를 제외</u>한 모두에게 전달

​	■OtherBuffered : <u>나를 제외</u>한 모두에게 <u>버퍼와 함께</u> 전달한다!

[매개변수 형식]-기본형식![img](https://static.wixstatic.com/media/1c4e22_e9200b0092664c47a4083e3a9ff21cd9~mv2.png/v1/fill/w_736,h_323,al_c,lg_1,q_90/1c4e22_e9200b0092664c47a4083e3a9ff21cd9~mv2.webp)

#### [PhotonMessageinfo 매개변수]

---

```c#
public class PlayerScript : MonoBehaviourPun
{
          PhotonView PV;

          void Start()
	{
                  PV = photonView;

 	      if(PV.ISMine) PV.RPC("TestRPC", RpcTarget.All, "A", "B");
             }

           void TestRPC(string value1, string value2, PhotonMessageInfo info)
              {
                   print(info.Sender.NickName + ", " + info.photonView.Owner.NickName + ", " + info.SentServerTime);
              }
}
```

##### ■info.Sender.NickName = 보내는사람을 인수로 받아온다.

##### ■info.photonView.Owner.NickName  = 받는사람의 포톤뷰의 이름을 인수로 받아온다.

##### ■info.SentServerTime = 받은 시간을 인수로 받아온다.

---

##### Resources

-[Photon멀티게임강의](https://www.youtube.com/watch?v=7tjez6oZDlA)
