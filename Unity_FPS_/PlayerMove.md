## PlayerMove 코드

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerMove : MonoBehaviour
{
    Transform mv;
    [SerializeField]
    private float v;
    private float h;
    private float PlayerSpeed = 10.0f;
    private float rotateSpeed = 50f;



    void Start()
    {
        mv = GetComponent<Transform>();
    }

  
    void Update()
    {
        v = Input.GetAxis("Horizontal");
        h = Input.GetAxis("Vertical");

        Vector3 PlayerPos = (Vector3.forward * v ) + (Vector3.left * h);
        ```

        mv.Translate(PlayerPos.normalized* PlayerSpeed * Time.deltaTime, Space.Self);

        mv.Rotate(Vector3.up * rotateSpeed * Time.deltaTime * h);
    }
}
```
