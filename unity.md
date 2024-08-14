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
	+ text 更改字体
		+ 相较于ui界面来说，游戏界面通常在左下角

+ tip
	+ 坐标球 scene右键overlay menu
	+ 
+ unity英语

+ idea
	+ 物体行进过程中下落

