#### 메뉴 관리 설정
---

**메뉴 열고닫기**
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

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
---

**무슨 메뉴를 열건지에 대해 인식 혹은 메뉴 상태인식**

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class MenuManager : MonoBehaviour
{
	public static MenuManager Instance; //전역으로 Menu의 변수또는 함수를 쓸 수 있게 만들어준다.

  [SerializeField] Menu[] menus;// menu스크립트를 가지고있는사람들 가져오기


	private void Awake()
	{
		Instance = this;
	}
	public void OpenMenu(string menuName)
	{
		for(int i = 0; i < menus.Length; i++)

			{
			if(menus[i].menuName == menuName)
				{
					OpenMenu(menus[i]); // 열려고 하는 메뉴 이름과 같으면 메뉴를 열기
				}
			else if(menus[i].open)
				{
					CloseMenu(menus[i]);
				}
	     	}
	}

	public void OpenMenu(Menu menu) // 메뉴가 열려있는지 확인후 open함수로 이동
	{
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
---
**photon 서버에 대한 기본 설정들**

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Photon.Pun;
using TMPro; // TMP를 읽어오기위한 메서드

public class Launcher : MonoBehaviourPunCallbacks // 플레이어 오버라이딩[기본세팅]
{
	[SerializeField] TMP_InputField roomNameInputField; // 방 이름 변수
	[SerializeField] TMP_Text errorText; //실패했을때 오류메세지 받아올 변수
	[SerializeField] TMP_Text roomNameText; //방 로드에 성공 했을때 이름 바꿔주는 변수
	void Start()
    {
        PhotonNetwork.ConnectUsingSettings();//포톤서버에 연결되어 한국지역에 고정됨 
    }

	public override void OnConnectedToMaster()//메인서버에 연결되었을때 실행되는 함수
	{
        PhotonNetwork.JoinLobby();//방을 참가하거나 방을 만들기전에 바로 로비에 참여하기
	}

	public override void OnJoinedLobby()//로비 안에 들어와서 실행되는 함수
	{
		MenuManager.Instance.OpenMenu("title");
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
	public override void OnLeftRoom()// 방을 떠났을때 실행
	{
		MenuManager.Instance.OpenMenu("title");
	}
	void Update()
    {
		

	}
}
```

---
