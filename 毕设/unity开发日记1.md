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
+ undo mesh renderer  ，取消网格渲染-->空气墙
+ panel 画布 下面单独加text
+ 找不到panel启动妈的好怪

+ idea
	+ 物体行进过程中下落
	+ 不拖组件怎么调用 https://ask.csdn.net/questions/7769320/53870024

#### 9.22
+ 欸吗我这拖延症，什么开发日志，ddl日志了这属于
+ 继续panel，panel是画布，适应屏幕
+ debug了一下endline，endline方块加了obstacle的tag导致和collision这个script冲突，导致画布不显示。然后panel要先设置为不显示，endline用到的函数OnTriggerEnter()要在属性碰撞里设置为is trigger
~~~
using UnityEngine;
using UnityEngine.SceneManagement;

public class LevelComplete : MonoBehaviour
{
    // 假设这个方法在某个事件（如玩家完成关卡）后被调用  
    public void LoadNextLevel()
    {
        // 获取当前激活的场景的索引  
        int currentSceneIndex = SceneManager.GetActiveScene().buildIndex;

        // 尝试加载下一个场景。注意要检查索引是否超出了场景的总数  
        int nextSceneIndex = currentSceneIndex + 1;
        if (nextSceneIndex < SceneManager.sceneCountInBuildSettings)
        {
            SceneManager.LoadScene(nextSceneIndex);
        }
        else
        {
            // 如果已经是最后一个场景，可以选择加载第一个场景或者做其他处理  
            Debug.Log("已经是最后一个场景了！");
            // 例如，加载第一个场景  
            // SceneManager.LoadScene(0);  
        }
    }
}
~~~
+ window->animation，选中panel进入记录模式创建关键帧，并调用下一个场景（tip1 要在动画里引入panel下下一个场景调用的script项目 （tip1在构建里设置场景顺序


#### 9.23
+ 做个类似猫猫头的编辑器工具
+ menu逻辑：新建的scene，再panel下做了button，script放在panel上，然后两个button的click引用panel，在选择其下function，这样不同button可以写在一个script
+ edit->project settings 可以在quality里设置游戏的渲染等级，player里设置游戏icon，鼠标，分辨率等
+ **导出有个问题欸** 他页面不是自适应emmm，要在研究一下
+ 还得多看看啊，面向对象的逻辑
+ [关于unity存储应该单独看一下](https://blog.csdn.net/xiaobao4106/article/details/138105663)
+ 热更

#### 9.23 
+ projectsettings->input manager ,替换字符，比方说space在代码里可写jump

#### 10.22
+ ...
+ 昨天忘记mark了，一会儿写上面
+ spirit动画，png导入可以选择mulitple切割获取，filter过滤器mode选择point就看得清了
+ 动画链接：在player下建立了一个animation用于sprite renderer插件，对此插件建立多个animation，在animator里对不同animation建立transition，并添加parameters作为条件字段为transition建立condition。然后对主player scipit建立animation关联。（他代码写得超级舒服！！明天放上来！！
+ ALT+ENTER:一键提取并创建方法
+ 
#### 10.23
+ 视频少看20s，埋头复盘2h
+ flip翻转和创建layermask地面图层用来检测，让其只跳一次
+ 


[以下视频参考](https://www.bilibili.com/video/BV1cM4y1p7RF?spm_id_from=333.788.player.switch&vd_source=e10f51470a19ec8e4125b51b7fdb73bb&p=19)
#### 11.28
+ 每日忏悔.jpg，北京挺好看的
+ 调整了一下character动态，movespeed和jumpforce调高，2d刚体的gravity scale调高，就能快速下落
+ 动画部分mark了一下，blendtree参数没搞明白


#### 12.2
+  冲刺时间 ：就是输入按键后，用dashtime和dashduration两个数来计时，duration设置冲刺的时间，time用来减减充当计时器，然后用dashspeed设置冲刺时的速度
``` 
        dashTime -= Time.deltaTime;//冲刺检测
        dashCoolDownTimer -= Time.deltaTime; ;
        if (Input.GetKeyDown(KeyCode.LeftShift) || Input.GetMouseButtonDown(1) && dashCoolDownTimer < 0)
        {//鼠标右键
            dashCoolDownTimer = dashCoolDown;
            dashTime = dashDuration;}
------------------------------------------------------------------------
        if(dashTime > 0)
        {rb.velocity = new Vector2(movespeed * dashSpeed* facingdirection, 0);}
        else
        { rb.velocity = new Vector2(movespeed * xinput, rb.velocity.y);}

```
+ 动画结束添加事件，新建了script，拖入关联animtor，从父类script里调用了animationover；动画编辑界面新建event就好
+ ctrl r 和ctrl f


+ #### 12.3
+ 先把骨骼和反向动力学看一下
+ psb图层，png单张

#### 12.4
+ 继续看unity那个，顺便把小蜘蛛那个代码看一下

#### 12.5
+ 继承 inheritance
```
父类文件名entity
//procected 这是一个访问修饰符，子类和派生类可见，其他不可见
//virtual 这意味着它可以在派生类中被重写（override）
//override：这个关键字表示当前的方法重写了基类中的一个方法
    protected virtual void Update()
    {
        GroundCollisionChecks();
    }
-------------------------------------------------------------
public class player : Entity{
...
    protected override void Start()
    {//protected：这是一个访问修饰符，表示这个方法只能在当前类或者派生类中被访问
     //override：这个关键字表示当前的方法重写了基类中的一个方法
        base.Start();//调用基类
    }
}
```

#### 12.6
+ 嗯嗯嗯封装继承多态嗯嗯嗯
+ 这个gizmos的射线很有意思,这里做了一个play检测，有点意思，之后可以研究一下
```
 private RaycastHit2D isPlayerDetected;//此射线用于检测位于射线路径上的对象
isPlayerDetected = Physics2D.Raycast(transform.position, Vector2.right, playerCheckDistance * facingdirection, whatIsPlayer);

图像看
Gizmos.DrawLine(transform.position, new Vector3(transform.position.x+playerCheckDistance*facingdirection,transform.position.y));
```

#### 12.7
+ 要学习的话，每日过数据结构，明天继续看数据库和c的string，那个blender和动画化程序pcb吗是叫也可以啊看起来了



