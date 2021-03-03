#### Photon기본설정
---
   
```
using Photon.Realtime;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Photon.Pun;
using TMPro; // TMP를 읽어오기위한 메서드
using System.Linq;


//이 스크립트에서 방을 떠나거나 들어왔을때의 이벤트를 구현

public class Launcher : MonoBehaviourPunCallbacks // 플레이어 오버라이딩[기본세팅]
{
	public static Launcher Instance;

	[SerializeField] TMP_InputField roomNameInputField; // 방 이름 변수
	[SerializeField] TMP_Text errorText; //실패했을때 오류메세지 받아올 변수
	[SerializeField] TMP_Text roomNameText; //방 로드에 성공 했을때 이름 바꿔주는 변수
	[SerializeField] GameObject roomListPrefab;
	[SerializeField] Transform roomListContent;//위치
	[SerializeField] GameObject PlayerListPrefab;
	[SerializeField] Transform PlayerListContent;//위치
	void Start()
    {
        PhotonNetwork.ConnectUsingSettings();//포톤서버에 연결되어 한국지역에 고정됨 
    }
	private void Awake()
	{
		Instance = this;	
	}

	public override void OnConnectedToMaster()//메인서버에 연결되었을때 실행되는 함수
	{
        PhotonNetwork.JoinLobby();//방을 참가하거나 방을 만들기전에 바로 로비에 참여하기
	}	

	public override void OnJoinedLobby()//로비 안에 들어와서 실행되는 함수
	{
		MenuManager.Instance.OpenMenu("title");
		PhotonNetwork.NickName = "Player " + Random.Range(0, 1000).ToString("0000");

	}

	public void CreateRoom()
	{
		if(string.IsNullOrEmpty(roomNameInputField.text))// 방의 이름이 비어있으면 재할당시킴
		{
			return;
		}
		PhotonNetwork.CreateRoom(roomNameInputField.text);//방의 이름이 할당이 될때 방을 만듬
		MenuManager.Instance.OpenMenu("loading");
	}

	public override void OnJoinedRoom() //방에 참여했을경우
	{
		MenuManager.Instance.OpenMenu("room");
		roomNameText.text = PhotonNetwork.CurrentRoom.Name;

		Player[] players = PhotonNetwork.PlayerList;

		for (int i = 0; i < players.Count(); i++)
		{
			Instantiate(PlayerListPrefab, PlayerListContent).GetComponent<PlayerListItem>().SetUp(players[i]);
		}
	}

	public override void OnJoinRoomFailed(short returnCode, string message)//방 참여에 실패했을경우
	{
		errorText.text = "Room Creation Failde : " + message;
		MenuManager.Instance.OpenMenu("error");
	}

	public void LeaveRoom()
	{
		MenuManager.Instance.OpenMenu("loading");
	}

	public void JoinRoom(RoomInfo info)
	{
		PhotonNetwork.JoinRoom(info.Name);
		MenuManager.Instance.OpenMenu("loading");
	}

	public override void OnLeftRoom()// 방을 떠났을때 실행
	{
		MenuManager.Instance.OpenMenu("title");
	}

	public override void OnRoomListUpdate(List<RoomInfo> roomList)
	{
		//-로비에 접속 시
		//-새로운 룸이 만들어질 경우
		//- 룸이 삭제되는 경우
		//-룸의 IsOpen 값이 변화할 경우
		foreach (Transform trans in roomListContent)
		{
			Destroy(trans.gameObject);
		}
		for(int i = 0; i < roomList.Count; i++)
		{
			Instantiate(roomListPrefab, roomListContent).GetComponent<RoomListItem>().Setup(roomList[i]);//플레이어 이름 할당
		}
	}

	public override void OnPlayerEnteredRoom(Player newPlayer)
	{
		Instantiate(PlayerListPrefab, PlayerListContent).GetComponent<PlayerListItem>().SetUp(newPlayer);
	}
	void Update()
    {
		

	}
}
```
  
#### 버튼이 클릭되었을 때 나타나는 이벤트, 여러번 열리면 안되는 메뉴 확인
---
  
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

//버튼이 클릭되었을때 나타나는 이벤트들, 여러가지 열림닫힘 여부 확인

public class MenuManager : MonoBehaviour
{
	public static MenuManager Instance; //전역으로 Menu스크립트의 변수또는 함수를 쓸 수 있게 만들어준다.
  [SerializeField] Menu[] menus;// menu스크립트를 가지고있는스크립트들 가져오기


	private void Awake()
	{
		Instance = this;
	}
	public void OpenMenu(string menuName)//버튼으로 넘겨받은 메뉴이름처리
	{
		for(int i = 0; i < menus.Length; i++)

			{
			if(menus[i].menuName == menuName)
				{
					OpenMenu(menus[i]); // 열려고 하는 메뉴 이름과 같으면 메뉴를 열기, 여기서 대조되는 이름은 전에 배열에서 지정해줬던 이름과 버튼클릭시 대입되는 이름
				}
			else if(menus[i].open)
				{
					CloseMenu(menus[i]);
				}
	     	}
	}

	public void OpenMenu(Menu menu) // 메뉴가 열려있는지 확인후 open함수로 이동
	{
		//매뉴가 계속해서 열리는지 확인
		for (int i = 0; i < menus.Length; i++)
		{
			if (menus[i].open) //메뉴가 열려있으면
			{
				CloseMenu(menus[i]);// 메뉴는 한번만 실행되야 하기 때문에 닫아줌
			}
		}
		menu.Open();
	}

	public void CloseMenu(Menu menu) // 메뉴가 닫혀있는지 확인
	{
		menu.Close();
	}
}
```
  
#### 메뉴열림닫힘확인후 메뉴 나타나게함
---
  
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

//메뉴의 실행여부 확인탭

public class Menu : MonoBehaviour
{
	public string menuName;// 각 오브젝트에 이름 할당해주기
    public bool open; // 메뉴가 열려 있는지 확인
  public void Open() //메뉴가 열려있는지 확인하고, 각각의 창에 있는 오브젝트를 나타나게해줌
	{
		open = true;
		gameObject.SetActive(true);
	}

	public void Close() //메뉴가 닫혀있는지 확인하고, 각각의 창에 있는 오브젝트를 숨기게 해줌
	{
		open = false;
		gameObject.SetActive(false);
	}
}
```
  
#### 플레이어가 방에 들어올때 닉네임대입
---
  
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Photon.Pun;
using Photon.Realtime;
using TMPro;

//플레이어가 방에 들어올때 닉네임 뜨게만듦

public class PlayerListItem : MonoBehaviourPunCallbacks //호출뒤 파괴
{
	[SerializeField] TMP_Text text;
	Player player;
    public void SetUp(Player _player) 
	{
		player = _player; // 현제 포톤서버에있는 닉네임을 Player변수에 지정
		text.text = _player.NickName; //전해진 닉네임을 문자에 저장
	}

	public override void OnPlayerLeftRoom(Player otherPlayer)
	{
		if(player == otherPlayer)
		{
			Destroy(gameObject);//방을 나갈시에 해당 닉네임 삭제
		}
	}

	public override void OnLeftRoom()
	{
		Destroy(gameObject);//방을 나가면 플레이어 목록 삭제
	}
}
```
  
#### 방 이름 받아오기
---
  
```
using Photon.Realtime;
using System.Collections;
using System.Collections.Generic;
using TMPro;
using UnityEngine;

//방 이름 받아오기

public class RoomListItem : MonoBehaviour
{

	[SerializeField] TMP_Text text;

	RoomInfo info;

	public void Setup(RoomInfo _info)
	{
		info = _info;
		text.text = _info.Name;
	}

	public void OnClick()
	{
		Launcher.Instance.JoinRoom(info);
	}
}
```
