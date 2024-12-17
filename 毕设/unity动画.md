+ spirit动画，png导入可以选择mulitple切割获取，filter过滤器mode选择point就看得清了
+ 在character下单独创建empty，改名为animtor，把spirite renderer部分放到animator下，把显示动画和物体运动分开来
+ 创建animator controller，拖到上一条的animtor上。
+ create animation 拖入spirite，可调节samples帧率，在同一个animation下可以create new clip添加同一角色不同状态
+ 用animator设置状态转换，在parameters设置参数，画箭头，在箭头下设置conditions，上面settings修改动画切入切出时间，然后写代码与unity条件一致
```
 public Animator anim;

//start里获取        
anim = GetComponentInChildren<Animator>();
//update里调用
AnimatorControllers();//封装啦

private void AnimatorControllers()
    //封装啦
    {
        ismoving = rb.velocity.x != 0;
        anim.SetFloat("Yvelocity",rb.velocity.y);
        anim.SetBool("ismoving", ismoving);
        anim.SetBool("isgrounded", isgrounded);
    }
```

+blend tree 混合树，emm就是链接两段动画，会自动生成一个blend parameters，具体参数还没搞明白，我不懂他那个对y轴正负判断是怎么判定的。。

+ 动画结束添加事件，新建了script，拖入关联animtor，从父类script里调用了animationover；动画编辑界面新建event就好




+ empty到橙色，橙色就是默认状态
+ 跳跃：anystate转换时，相当于isgrounded一直是false，取消can transition to itself，防止持续对自己转换导致卡在第一帧
+ 一般can transition to itself，durationtiome，hasexittime设置为0


### 骨骼绑定和反向动力学
+ 创建ik2dmanager后是按照当前componet的父辈去选择点的，
+ 两个chain无法选中尾端点，强行引用的化会导致无法旋转，这时候解决的话可以再在末端创建一个小骨骼，
+ ccd不改变骨骼关节方向，fabrik改变了骨骼方向，limb相当于简洁版
+ 我悟了，chain是应用于多个点，点少的时候就会有僵硬的情况，所以点少请用imb：）
+ limb需要