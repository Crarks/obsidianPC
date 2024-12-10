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
+ playststemachine，像是用来初始化的状态转换控制文件
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
+ playerstate 具体状态执行
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


+ #### 12.10
+  crtl+d复制当前行 alt+上下将当前行上下移动
+ 关于animation的逻辑，wc有点妙,真的吧面向对象发挥到极致
```看9号那个play而的awake，把idle对new的两个对象进行了赋值
	看9号的playerstate，s'n

```