# 方块
+ 物体运动
	 ```c#
	 if (Input.GetKey("a"))
        {rc.AddForce(-go * Time.deltaTime, 0, 0,ForceMode.VelocityChange);
        }
	```
+ 创建 
	+ 材质 material physicmaterial 
	+ 物体的副本
	+ fog window-rendering-light
	+ collision detection 碰撞检测选项 project setting里time有一个fixed timestep （适用于频繁更新模型防止穿模吗emmmm？
+ 相机
	 ```
	public Transform player; // 获取玩家的transform值  
    public Vector3 offset; // 相机相对于玩家的偏移量,包含三个值
    void Update()
    {
        // 只更新相机的位置，不更新旋转  
        transform.position = player.position + offset;
	 ```
+ 碰撞
	```
		public class collsion : MonoBehaviour
	{
	    public move collisionmove;
	    private void OnCollisionEnter(Collision collision)// 接受cube碰撞信息
	    {
	        Debug.Log(collision.collider.name);
	  /*      if (collision.collider.tag == "obstacle" )//碰撞即停止物体运动
	        {         collisionmove.enabled = false;}
	  */}}
	```
+ UI
	+ text 更改字体 canvas
		+ 相较于ui界面来说，游戏界面通常在左下角
```
using UnityEngine.UI;
public class score : MonoBehaviour
{
    public Transform player;//获取行进距离判断分数
    public Text scoreText;
    // Update is called once per frame
    void Update()
    {
       scoreText.text = "z: " +  player.position.z.ToString("0");
    }}
```  
+ TMP
			+ https://tieba.baidu.com/p/7625369037

+ tip
	+ 坐标球 scene右键overlay menu
	+ 
+ unity英语



之后按照每日来记，连连摇头啊我
#### 8.14
+ canvas 添加text，有text和tmp的区别，写在上面ui那里
+ 添加 结束endgame，先是创建了一个emptyobject，命名为gamemanager，以便可以在unity内部进行数值调用，然后分别在需要添加end的地方调用与gamemanager相关联的script，比方说物体碰撞scrpit，和物体运动script 运动超过范围时触发场景调用。
+ 关于调用，不建议在unity里拖动敖，用下面那个调用的语句互相调用敖。。。
```
using UnityEngine;
using UnityEngine.SceneManagement;
public class GameManager : MonoBehaviour{
    bool gameHasEnded = false;
    public float restartDelay = 3f;
    public void EndGame(){
        if (gameHasEnded == false)
        {
            gameHasEnded = true;
             Debug.Log("Game Over");
            Invoke("Restart", restartDelay);}
    }
   void Restart(){
  SceneManager.LoadScene(SceneManager.GetActiveScene().name);
    }
}
//调用的语句  FindObjectOfType<GameManager>().EndGame();
```

+ build setting 添加场景不知道干嘛的


#### 8.15
+ undo mesh renderer\
+ panel

+ idea
	+ 物体行进过程中下落
	+ 不拖组件怎么调用 https://ask.csdn.net/questions/7769320/53870024

