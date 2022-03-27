#  不要忘记自己的算法比赛，你是个软件开发者
本篇教程均已sunny land 为实验对象
自由创造，


## 添加背景，绘制地图，调整图层
- 点中图片调整像素


- 取消图片背景显示

![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-25-17-49-15.png)

- 如果素材是png格式的，它会自动切割，不需要以前的手切了
![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-25-18-05-33.png)
- 每个像素16，直接一格一格地切，比上面那种方便灵活使用素材
- ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-25-18-08-30.png)
- ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-25-18-08-02.png)


- maicamera中调整大小，使得游戏场景更多
- ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-25-18-28-46.png)

- 排序图层
- ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-25-18-32-15.png)
- 越在下越显示在前面
- 图层顺序就是越大越在前面


##  添加人物
同读懂脚本第一期教程

### 关于输入的按键设置
- 在项目设置里面，我们可以更改哪个键负责什么指令
- ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-25-19-18-21.png)

- 老规矩：2d人物冻结旋转
![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-25-19-32-33.png)

- 如果在游戏中调好了效果，需要在退出游戏后依旧保存这些，就需要使用
![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-25-19-42-46.png)

- 如何判断人物面向哪里，进而有一个动画的改变，使用松鼠当样例
# 人类的伟大之处就是勇气的伟大之处。

## 为什么人物移动会有卡顿感，老问题
- (一)  我们给整个地图赋予了Tilemap Conllider 2D ,它把每个小瓦片都整成一个个碰撞体，人物也是个碰撞体，中间可能就是会移动出现卡顿，卡在我们看不到的地方
- 记得修改检测地面碰撞的碰撞器为圆形碰撞器
- ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-26-12-28-18.png)
- (二) 提供另一种解决方法：为人物添加二种碰撞体，一种box Collider 2d ,一种 Circle collider 2d
- 还有一种，就是读懂脚本第一期的方法，为tilemap 添加，进行合并下的碰撞体，将不需要碰撞的改为触发器即可。



## 动画部分
1. 给相应的角色添加animator组件，该组件需要一个动画控制器
2. ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-25-22-52-06.png)
3. 在合适的文件夹下创建animeator 动画控制器 ，给动画组件赋值，如图
4. ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-10-20-57.png)
5. 按如图方式打开动画编辑窗口
 ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-25-22-53-41.png)
4. 选中目标角色，开始创建动画，创建动画存于相应的文件夹
5. ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-25-22-59-48.png)     把创建动画需要的文件图片拖入动画
6. 如图![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-25-23-26-48.png)
7. 在动画器中可以看到已经添加的动画
![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-25-23-29-03.png)

8. 创建新的动画 点击“新的剪辑”
![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-25-23-37-24.png)
-  意外发生：
   -  这是由于没有更改run图片的单位像素。
    -    ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-26-00-18-40.png)

9. 为了循环播放动画效果，我们需要勾选上"loop time",即"循环时间"，
![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-26-00-23-54.png)

10. 如何连接各个动画呢？
    - 点击动画，‘创建过渡’
    ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-26-09-36-03.png) 
    -  在这些箭头之间，我们就可以设置一些条件让其来回切换
    ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-26-09-51-31.png)
    - 设置参数!
    - ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-26-09-52-52.png)
    - ‘过渡持续时间’  ‘有退出时间’改为0，动画之间切换，就随停随起
    - 设置条件- 速度小于0.1 就是停止  ，对于0.1,就是跑动
    - 参数设置完毕，如何控制参数？
    - 修改脚本
```c#
 public Animator anim;  接受动画组件

 //修改跑动状态参数
  anim.SetFloat("running", Mathf.Abs(facedirection));//设定参数值 
```
    - 拖动动画组件到anim中  ，![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-26-10-28-50.png)
    - 有些时候动画效果不对，也可能是自己创建动画效果时，拖入的图片错误。
- # 添加跳跃动画  分为jump 和fall  添加完动画切片 
  - 创建过渡  ，跑动、站立的时候都可以跳跃  落地之后就应该站立 
  - 添加过渡的参数   ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-26-11-22-38.png) 
  - 老规矩 编辑过渡的信息，没有退出时间，没有过渡持续时间 
  - 切换到跳跃的这个条件就是，jumping 参数  为true 在脚本中设置jumping参数
```c#
        anim.SetBool("jumping", true);//设置 其它状态到跳跃过渡的参数
```
- # 添加fall动画过渡
- 与过渡到跳跃不同的是，过渡到falling时,需要把falling 设为true ,jumping 设为false
- ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-26-11-36-07.png)
- 不要忘了给fall 到 idle  过渡添加条件  **所以说，每个过渡都需要添加参数，修改退出时间，过渡持续时间**
- ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-26-11-40-05.png)
- # 后面判断落地切换动画，有点复杂，后面直接贴代码吧
    - 创建新的图层，Ground 
    - ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-26-12-05-20.png)
    - 修改tilemap 图层为Ground  
    - ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-26-12-05-04.png)
```c#
//贴一下代码吧
    public Collider2D coll;//将人物中的box Collider 2D 添加到这里
    public LayerMask ground;//判断落在地面

void SwitchAnim()
    {
        anim.SetBool("idle", false);

        if(anim.GetBool("jumping"))
        {
            if (rb.velocity.y < 0)//说明没跳了
            {
                anim.SetBool("jumping", false);
                anim.SetBool("falling", true);
            }
        }//不在jumping了
        else if (coll.IsTouchingLayers(ground)){//判断是否碰撞到地面这个图层
            anim.SetBool("falling", false);
            anim.SetBool("idle", true);
        }
    }
```

## 使用Cinemachine
1. 导入包 ，创建对象，将人物拖到follow里
![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-26-14-01-05.png)
2. ## 介绍参数
    - Dead Zone 死锁区域，调整了之后，人物在死锁范围内移动，摄像机不移动  --- *可以实现镜头跟踪效果*
    - ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-26-14-04-43.png)
    - 调整Screen X ,Y 使得出现摄像头居左或者居右的效果

    - ### 限制摄像机显示范围，避免出现场景之外的画面
    - 选中 Cinemachine Confiner  记住“add Extension” 中的 select ,不是添加组件  
    - ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-26-18-16-44.png)
    - 为backImage背景添加collider 限制摄像机显示范围  ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-26-18-19-53.png)
    - ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-26-18-20-35.png)
    - 调整点的边框，如果不需要某个点，按住ctrl 再点击即可进行删除
    - 回到我们的CM 摄像机，为confiner添加限制边界的组件对象
    - ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-26-18-28-09.png)
    - 记得勾选上多边形触发器的isTrigger 是触发器，不然人物会弹出去

## 创建道具---类似人物
### 统一使用sprite创建并渲染对象
**好处：节省渲染时间、提高效率，尤其是2d对象较多时。**

直接创建动画的话，就会自动给你创建动画控制器

很多东西与前面重复，跳过。

### 检测碰撞cherry ---脚本

- 如何判断碰撞的物品是cherry呢？
- 给cherry 添加标签(随便命名，没啥要求)
  - 添加标签
  - ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-10-41-56.png)*添加好后设置标签* *要添加标签也得点那里*
  - ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-10-41-25.png)*新建标签*

```c#
public int cherry = 0;//体积cherry 数量，可以改成甲骨文之类的
private void OnTriggerEnter2D(Collider2D collision)
    {
        //检测碰撞到的对象上的标签
        if (collision.tag == "Collection")//如果是cherry等的收集物品
        {
            Destroy(collision.gameObject);//销毁对象
            cherry += 1;
        }

    }
```


**提供一种以前的方法，该脚本直接写在物品下面，通过检测被碰撞物品是否有对应脚本**
```c# 
/// <summary>
    /// 碰撞检测相关
    /// </summary>
    /// <param name="collision"></param>
    void OnTriggerEnter2D(Collider2D other)
    {
        //检测碰撞到的物品是否有对应脚本
        PlayerController pc = other.GetComponent<PlayerController>();
        if(pc!=null)
        {
            //调用对应的角色属性和方法 去实现目标  --- 需要在player里面添加新的属性和方法
            if (pc.MyCurrentHealthy < pc.MyMaxHealthy)
            {
                pc.ChangeHealth(1);
                Instantiate(collectEffect, transform.position, Quaternion.identity);//生成特效
                Audiomanger.instance.AudioPlay(collectClip);//播放音效
                Destroy(this.gameObject);//销毁当前的物品 this指针
                Debug.Log("玩家碰到了草莓!");
            }
            
        }
    }
```

## 添加图层，只有创作场景

![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-11-07-03.png)
不同图层可以用于实现人物被树遮挡出的效果

可以在不同的图层中排序，你调整的图层顺序就是每一个图层的细分的排序
![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-13-00-32.png)

自由创作，这里略过。

# 快捷键 Ctrl+z  撤销  Ctrl+y 恢复撤销的内容

### 解决人物撞墙不掉落问题
- 创建2D物理材质
![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-14-26-28.png)
- 然后将物理材质的摩擦系数设为0
![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-14-27-44.png)
- 为头部的碰撞盒添加自己做的物理材质
- ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-14-29-13.png)
- ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-14-29-32.png)

## 设置UI，以最终实现背包
1. 创建对象![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-15-09-20.png)
2. 在UI中创建txt  ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-15-12-41.png)
3. 然后输入想要显示的内容，调整字体、大小、居中等等文字方面的设置
4. ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-15-13-54.png)
5. 调整一下文字框大小
6. ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-15-15-00.png)
7. 以上，只能实现固定的内容显示  --- 实际中，物品数量是会变化的
8. UI代码：
```c#
//需要导入 using UnityEngine.UI;
    public Text CherryNums;

 private void OnTriggerEnter2D(Collider2D collision)
    {
        //检测碰撞到的对象上的标签
        if (collision.tag == "Collection")//如果是cherry等的收集物品
        {
            Destroy(collision.gameObject);//销毁对象
            cherry += 1;

            //更改text内容
            CherryNums.text = cherry.ToString();//将数字转为字符
        }
    }

```
9. 为CherryNums 赋予想要控制的文本   
![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-15-41-48.png)
10.   如图   ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-15-42-16.png) 
 
 基本实现收集樱桃，数字变化的效果

### 问题
![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-16-00-03.png)
并没有实现理想的文本居左上的效果，因为随着画面比例的变化就会出现这些问题。

如何实现定位呢？
![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-16-08-04.png)
 - 那个像伞一样的符号就是 瞄准点 ，随着画面变化，距离却不会有任何变化。于是，就错位了。
 - 解决方法：
 - 选中要修改的文本,打开这个画面
- ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-16-21-14.png)
- 选中一直要锁定的点，如图即可。
- ![d:\Program Files\Unity Project\C# 脚本学习记录\第二篇文章](images/2022-03-27-16-22-53.png)














作业：实现钻石，用另一种方法 
搞定背包效果，每种怪兽的脚本
查看人物装备道具，其实这个也还好，但是我们需要在这个过程中，修改碰撞体类型
这个动画如何流畅。。。。


道具：
拾取增益：
1、肉：恢复生命值+10
2、鼎：盛有水，获得后速度+1
3、甲骨：拾取后有动画，展示文字记载，探索这个世界的秘密以及回去的方法，通过的关键道具 
4、武器系统：打败指定Boss后可获得，可选择是否装备，一旦选择将无法更改，只能等到下一次更换武器。


敌人：
*需要实现在一定范围内检测到人物产生敌意，追逐角色并进行攻击，*
--如此，需要判断敌人只能在那个场景移动，不能说跳跃啥的。
获得移动的边界，这块地的长度，它能移动的范围   --- 进行移动范围的限制

*只有消灭全部怪物才能进入BOSS关卡*   
--- 考虑在人物脚本中添加怪兽数量，怪兽每死一只，人物这里记录的怪兽数量进行改动，
为进入BOSS关卡添加一个怪物为0的限制。

敌人的