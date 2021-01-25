
싱글게임은 서로를 모름

멀티게임은 서로에게 영향을 준다!

<u> `ex)상대방의 능력치,체력등등 `</u>

포톤에서 모든 동기화는 [PhotonView]컴포넌트

## [PhotonView가 <u>씬에 배치된채</u>로 있는경우]

<img src="https://static.wixstatic.com/media/1c4e22_1e24d0c2c47247b295fd189a77712381~mv2.jpg/v1/fill/w_827,h_206,al_c,lg_1,q_90/1c4e22_1e24d0c2c47247b295fd189a77712381~mv2.webp" alt="img" style="zoom: 80%;" />

#### Owner : 소유자,<u>씬이 주인</u>이다.(씬에 배치되어있기때문!)

​	■Fixed - 고정

​	■Takeover - 클라이언트가 <u>그냥</u> 가져갈 수 있음

​	■Request - 주인에게 <u>허락 받아야</u> 가져갈 수 있음

#### View ID : 포톤뷰의 고유 ID, 씬에 배치된것은 1~999까지 가능,점차 1씩증가한다

​        ■Observe option - 동기화 옵션, off외에는 모두 Observed Components에 하나라도

 			            있어야함(아니면 오류생김!)

​		■Off - RPC만 사용할 경우(기본값)

​		■Reliable Delta Compressed - 받은 데이터를 비교해 <u>같으면 보내지 않음</u>

​		■Unreliable - <u>계속보냄</u>, 손실 가능성(계속 보내고 계속 받음)

​		■Unreliable  on Change - <u>변경이 있을 때</u> 계속 보냄 (보내긴 계속 보내지만 받는사

​           람이 변경이 있을때 보냄)

​		■Observed Components : 동기화할 컴포넌트 넣는부분

---

##### Resources

-[Photon멀티게임강의](https://www.youtube.com/watch?v=7tjez6oZDlA)
