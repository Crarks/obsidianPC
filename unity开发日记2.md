+ #### 12.8
+ 状态机 假设文件，player继承monobehavior在player里引用，playerstatemachine，playerstate，之后的playmovestate或者playidlesytate继承playerstate，也就是具体状态的描述   
+ player 用来对状态发出初始化指令和调用
```
public class Player : MonoBehaviour
{
    public PlayerStateMachine stateMachine { get; private set; }
    public  PlayerIdleState idleState { get; private set; }
    public PlayerMoveState moveState { get; private set; }
    private void Awake()//priority>start
    {
        stateMachine = new PlayerStateMachine();
        idleState = new PlayerIdleState(this,stateMachine,"Idle");
        moveState = new PlayerMoveState(this, stateMachine, "Move");
    }
    private void Start()
    {
        stateMachine.Initialize(idleState);
    }
    private void Update()
    {
       stateMachine.currentState.update();
    }
}
```
+ playststemachine，用来初始化和状态转换控制文件，多态，实际上状态转换时是这么调用的->stateMachine.ChangeState(player.moveState)。player.movestate传入的其实是在player文件awake里定义的playeridlestate，所以当他传递进去的时候，实际上先调用的是playeridlestate里的exit方法，再根据base继承到playstate里完成
```
public class PlayerStateMachine 
{
    public PlayerState currentState{ get; private set; }//readonly
    
    public void Initialize(PlayerState _state)
    {
        currentState = _state;
        currentState.Enter();
    }
    public void ChangeState (PlayerState _newState)
    {
        currentState.Exit();
        currentState = _newState;
        currentState.Enter();
    }
}
```
+ playerstate 具体状态执行，三个this，实际上跑的时候（看player）是没有调用到playerstate，是子类比如playeridlestate继承了父类，所以用this确认当前子类
```
public class PlayerState
{
    protected PlayerStateMachine stateMachine;
    protected Player player;

    private string animBoolName;

    public PlayerState(Player _player,PlayerStateMachine _stateMachine,string _animBoolName)
    {
        this.player = _player;
        this.stateMachine = _stateMachine;
        this.animBoolName = _animBoolName;
    }
    public virtual void Enter(){}
    public virtual void Update(){}
    public virtual void Exit() {}
}
```
+ alt+enter是个好东西
+ MonoBehaviour 只有继承自这个类的脚本，才有这些生命周期事件https://blog.csdn.net/weixin_45961836/article/details/134712845


#### 12.10
+  crtl+d复制当前行 alt+上下将当前行上下移动
+ 关于animation的逻辑，(每日bb：wc有点妙,真的吧面向对象发挥到极致，面向对象就在于封装继承多态，像player像是调用playidlestate，但实际上功能实现是在父类，就是继承和封装，然后在playstatemachine里的调用用到了多态！
```看9号那个player的awake和playerstate的awake，在player里对new的两个对象进行了赋值，然后在里用子类向上继承方法，playerstate只起到一个当前类的继承作用，很面向对象，单看代码不觉得，真的写起逻辑就是每个干每个的事儿
playstate文件
	    public virtual void Enter() 
    { player.anim.SetBool(animBoolName, true);}
        public virtual void Exit() 
    {    player.anim.SetBool(animBoolName, false);}
```
+ rigidbody掉了一下collision和interpolate俩个值
+ 、#region是一个分块预处理命令，它主要用于编辑代码的分段，在编译时会被自动删除

#### 12.10
+ rigibody 更像是物体本身属性，包括运动旋转velocity这样的，所以setvelociy这样的给rb赋值的直接写在player
+ player像是接口层，对外输出以及rigidbody这些component以及总体的调用，然后对于playeridlestate这样的就像是对象，个人以为playeridlestate这样的继承的，尽量引用数据都在playerstate父类里定义
+ 累了，记得添加layer和has exit time取消

#### 12.13
+ 细细一看，bug还挺多的，jump和air这俩状态很奇怪，然后上面应该再加一个空中状态，检测起跳时是否有输入，然后原地起跳后就不会像个柱子一样:(，总之还要做很多优化。
+ 刚说有问题他就解决了，到时候在air和jump的父里加上这个
+ if (xInput != 0)
        {
            player.SetVelocity(player.moveSpeed * xInput * .8f, rb.velocity.y);

        }
+        xInput = Input.GetAxisRaw("Horizontal");
        yInput = Input.GetAxisRaw("Vertical");

+ 这个状态机的运行状态还不是搞得很明白
```滑墙切跳墙不加return会被下面的if语句打断，怎么个事儿
        if(Input.GetKeyDown(KeyCode.Space))
        {
            stateMachine.ChangeState(player.wallJumpState);
            return;
        }
```

#### 12.16
+ 14号考6级，昨天给学弟配idea
+ 上次attack的实现，先是动画，在playerstate里设置了trigger，通过trigger的触发判断attack的状态与动画切换
+ 好奇怪，这个move状态和attack叠加了，这个是unity与运行的问题吗emmmmmm
+ 问题就是grounded里状态调用了attack之后，会回到move，重新把值赋成了move
```move里的顺序先修改一下，要不然base出来之后会把velocity改掉，巨tm奇怪捏吗，可能是attack攻击条件退出切换的问题吗？？？？？
    暂时这样改了
    public override void Update()
    {        
        player.SetVelocity(xInput*player.moveSpeed, rb.velocity.y);
        base.Update();
        if (xInput == 0 )
            stateMachine.ChangeState(player.idleState);
        
    }
```
+ 哈哈，破案了，是我zerovelocity没赋值给rb：）


#### 12.17
+ 我去这个tilemap好高级
+ 我的锅，这个virtualcarmea也好好用哈哈哈哈，然后这个相机运动轨迹不知道能不能参考一下
+ sorting layer
+ 这个视差滚动背景效果（Parallax Scrolling Background）还需要优化，我还想做一下那个泰拉瑞亚的地形切换
+ 

#### 12.18
+ 把背景的代码和流程过一下奥
+ ik
+ aaaaa生气，怎么找不到卡牌的udemy啊，有点想做密教模拟那个

#### 12.23
+ 去武汉玩了几天我干，怎么五天没学习了
+ 那个背景代码，说简单也挺简单的，就是把背景图跟相机的相对位置计算然后移动

#### 12.26
+ 昨天考试，好像胆汁反流，好痛苦
#### 12.28
+ 没学习也好痛苦，可是肚子真的不舒服，全身没力气
+ 角色实体状态机，角色攻击动作以及动画设计，敌人设计，技能设计，技能树，用户界面，物品状态影响，视觉效果

#### 2025.1.5
+ 好久没写代码晕了
+ 看一下那个enemybase是啥东西，确实好奇怪，两个在skeleton里都是this有啥区分的必要奥
+ 