#### 디자인패턴 - 싱글톤

  

> 임의의 클래스 즉, 내가 만든 싱글톤 인스턴스를 사용가능

  

[사용하는이유]

  1.클래스 구조를 짜다보면 다른 클래스의 함수를 이용하기때문에
	전체 클래스들이 공유하는 전역변수 필요

   2 .게임이 복잡해지면 클래스를 참조하는 변수가 증가

​    3.클래스 구조에서 공통적으로 사용하거나 게임전체를 관장하는 매니저 

 	클래스등은싱글톤으로 따로 빼는게 도움

  

```
[싱글톤을 사용하는 방법]
  
1.싱글톤 클래스가 Monobehaviour를 상속받아서 Hierarchy에 존재
2.Monobehaviour를 상속받지않고 Hierarchy에 존재하지 않음
```

  

**1.싱글톤 클래스가 Monobehaviour를 상속받아서 Hierarchy에 존재**

---

  

```c#
 	//게임매니저의 인스턴스를 담는 전역변수 즉, static 변수
    //이 게임 내에서 게임매니저 인스턴스는 이 instance에 담긴녀석만 존재함
    //[보안]을 위해 private으로.
    
    private static GameMgr instance = null;

    void Awake()
    {
        if (null == instance)
        {
            //이 클래스 인스턴스가 탄생했을 때 전역변수 instance에 게임매니저 인스턴스가 담겨있			      지 않다면, 자신을 넣어준다.
            instance = this;

           
            DontDestroyOnLoad(gameObject);
            //씬 전환이 되더라도 파괴되지 않게 DontDestroyOnLoad를 붙인다.
        }
        else
        {
            //만약 씬 이동이 되었는데 그 씬에도 Hierarchy에 GameMgr이 존재할 수도 있다.
            //그럴 경우엔 이전 씬에서 사용하던 인스턴스를 계속 사용해주는 경우가 많은 것 같다.
            //그래서 이미 전역변수인 instance에 인스턴스가 존재한다면 자신(새로운 씬의 					  GameMgr)을 삭제해준다.
            Destroy(this.gameObject);
        }
    }
```

   

이렇게 된다면 모든 클래스에서 GameMgr라는 변수를 다음과같이 수정 할 수있다.

   

```
GameMgr.Instance.[변수명]
```

  

**2.Monobehaviour를 상속받지않고 Hierarchy에 존재하지 않음**

---

  

```c#
   private static GameMgr instance;

    //게임 매니저 인스턴스에 접근할 수 있는 프로퍼티. static이므로 다른 클래스에서 맘껏 호출할 수 		있다.
    public static GameMgr Instance
    {
        get
        {
            if(null == instance)
            {
                //게임 인스턴스가 없다면 하나 생성해서 넣어준다.
                instance = new GameMgr();
            }
            return instance;
        }
    }
```

​    

> Monobehaviour를 상속받지 않는 경우의 좋은 점

​    

1.씬 이동시의 신경을 쓰지 않아도 된다. 씬이동을 했을때에 같은 싱글톤 클래스가 있다면 신경 써줘야하는                

새로운 씬의Hierarchy에 있는 인스턴스를 쓸지를 선택을 안해도 된다.

2.현재 버전의 유니티오브젝트라면 모두 가지게될 Transform 컴포넌트를 

가지지 않아서 메모리 점유를 차지하지않아 메모리에 도움을 준다.

  

> 싱글톤의 문제점

  

클래스들과 싱글톤, 그리고 싱글톤이 가지고 있는 클래스 인스턴스들간의 의존도가 복잡해져서 

게임 업데이트를 하려면 게임 전체를 갈아엎어야 될 수도 있다.

  

또한 싱글톤은 게임이 종료되지 않는 한 계속해서 메모리를 점유하고 있으므로, 

싱글톤의 남발은 `메모리를 비효율적`으로 사용하게 한다.
