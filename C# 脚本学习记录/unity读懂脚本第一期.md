# 我永远向往着创造奇迹的人
本记录均已ruby adventrue 作为实验游戏对象
## 任务目标
游戏大体框架，素材动画不用搞用别的代替，先让小人能跑能跳能打怪开背包掉血

### 待解决的技术问题
- 背包打开过程中的脚本，我打开一个背包，要能看到里面的物品数量，以及我能做出选择。
- 摄像头调整镜头为侧视图那种，不是俯视图。
- 实现使用普通的图片，拼凑地图    *半完成，还需要调整碰撞参数*
- 尝试使用物品小标志当做自主设置怪物的练习，并赋予脚本，属性，触发器 
- 设置关节之间的入口，出口，考虑到可能到需要动画

今晚先把之前的代码搞定，后面再找个2d游戏做做
## 功能需求
wasd  上下左右移动
space 空格跳跃

## 所谓的关卡设计
当然这并不是一个好做的事情

## 研读代码

### 移动代码部分
```c#
//======移动==============
void start()
{
        robody = GetComponent<Rigidbody2D>();//获取到了人物的刚体组件
}
//思路是：用刚体的移动代替人物的移动，用以解决人物抖动问题(本身人物和刚体是一体的,这样移动是可以的)
void fixuedUpdate(){
        float moveX = Input.GetAxisRaw("Horizontal");//控制水平移动方向，A:-1 D:1
        float moveY = Input.GetAxisRaw("Vertical");//控制垂直方向  W:1 S:-1 不按:0
        //以上，使用方向键上下左右也是一样的
        Vector2 moveVector = new Vector2(moveX, moveY);
        Vector2 position = rbody.position;
        position += moveVector * speed * Time.deltaTime;
        //deltaTime 改为 fixedDeltaTime 的确会变快，这适用于某些版本的bug，可以把速度调正常
        rbody.MovePosition(position);
}
```

```c#
//上下左右移动
//没有使用刚体的移动，不完善版本，后期加了各种组件，会有不好的效果
void update(){
        float moveX=input.GetAxisRaw("Horizontal");//控制谁水平
        float moveY = Input.GetAxisRaw("Vertical");

        Vector2 position = transform.position;
        position.x +=moveX*speed*Time.deltaTime; 
        position.y +=moveY*speed*Time.deltaTime;
        transform.position=position;
}
```

### 如何连接图片资源和Tilemap
2020版unity不需要创建Tiles,拖动到tile palette里面自动创建tiles(瓦片)

![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-10-11-30.png)
*打开平铺调色板*

![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-10-14-25.png)
*创建新的平铺调色板，可以用于存放不同的素材类型*

#### 将图片进行分割
首先导入本地图片，选中图片，将单个改为多个，
![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-11-49-13.png)
，使用精灵编辑![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-11-50-23.png)，然后选中切片，将类型从自动改为Grid By Cell Count,![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-11-54-19.png).
修改行与列为3*3，即切成9片，![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-11-55-13.png)

可以选中多张图片，将Sprite 模式(精灵模式)改为多个，但依旧需要一张一张图片的切割

另一种切割方式：Grid By Cell Size，表示按照大小进行切割
I will try!

细节问题：
- 所以图片要制作成2的n次方像素。
- [Unity导入图片尺寸大小和压缩格式的问题](https://blog.csdn.net/linxinfa/article/details/108827197?utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~aggregatepage~first_rank_ecpm_v1~rank_v31_ecpm-2-108827197.pc_agg_new_rank&utm_term=dxt%E6%94%AF%E6%8C%81%E7%9A%84%E5%9B%BE%E7%89%87%E5%83%8F%E7%B4%A0%E5%A4%A7%E5%B0%8F&spm=1000.2123.3001.4430)

- [使用tilemap绘制场景](https://blog.csdn.net/Lmz_0314/article/details/121863847)
这篇教程还是有用的。

接下来把图片拖入tile palette中，就可。然后使用各种工具绘制地图即可。
注意：
![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-17-22-51.png)
当你有多个tile palette时，需要注意图层顺序，比如背景的图层![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-17-24-49.png)顺序就最低，其它的什么就高一些

### 添加物品丰富地图
- 概念：玉质体：直接讲作用，在Assets文件夹下创建一个Prefabs文件夹，即为玉质体文件夹，把你会反复用到的物品组件拖入其中，(举例子：果树，你调整了参数，保存，后面你从玉质体中拖入的果树都具有同样的性质，不再需要一棵一棵地调整参数，什么碰撞触发器、挂载脚本之类的),方便你后面直接使用。

![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-19-54-30.png)
在玉质体做了修改了，选择‘覆盖’，‘应用所有’，即对所有这种物品做出这个改变。


结论:将自己想当做组件的变成png格式，在调整大小，就可以了。当然也可以直接修改每单位像素点，处于保险，我没怎么尝试。
### 人物改造
对于角色是需要添加一个2d刚体的，Rigidbody 2D .  然后是Box Collider 2D盒状碰撞器

### 物品改造
- 添加组件：box conllider 2d碰撞器  一定是2d,不然不起作用！！！

![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-19-41-34.png)
选中它，编辑碰撞作用范围。

#### 小插曲，修改图层排序
为了能够让同一图层之间有层次感，举例子：我一个任务走到树后面，结果画面上人物还是在树前面，没有被树遮挡，这不合理，好吧。故需要调整层级点击‘编辑’，选中‘项目设置’，
![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-20-35-14.png)

在unity右边的‘project setting’中的‘图形’中，修改‘摄像机设置’中的‘透明排序轴’改为y轴。(2d的游戏，z轴应该没有用，就像为了防止人物碰撞时受力导致旋转，一般都会锁定z轴。如图：

![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-20-46-38.png)
)
![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-20-40-09.png)

#### 整理游戏资源
页面上太多物体，可以创建一个空物体，然后把同类型的物体都放在这个空物体下。
![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-21-01-03.png)

#### 物体下坠 
如果物体下坠的话，把刚体中的重力改为0


### 设定实现人物不在水面上移动----人物不在障碍上移动
1. 选中tilemap，![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-21-51-32.png)，给整体添加tilemap conllider 2d，但是这样子会让人物与整个地图进行碰撞，进而人物不能再移动
2. 解决方案：打开你之前存放瓦片资源的文件夹，![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-21-56-31.png)，选中那些地面(除开那些你想让它碰撞的瓦片)，修改‘碰撞器类型’为‘none’ --- ‘无’
3. 如图：![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-21-57-24.png)
   1. 存在的问题：我们给每一个瓦片都整了个单独的碰撞器，有些消耗性能。如何优化？
   2. 优化方法：选中‘tilemap’对象，添加组件 ‘Composite Collider 2D’,(在添加该组件时，会自动给tilemap对象添加‘Rigidbody 2D’组件，正常情况，不要忘了取消‘Rigidbody 2D’的重力，或者将地图背景Tilemap中‘Rigidbody 2D’刚体的身体类型设置为静态，不然地震效果！！！)
   3. 然后在‘Tilemap Collider 2D’中选中‘由复合使用’，![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-22-07-38.png)，如图。
   4. 如此便可，将一块区域(比如：水塘)分散的碰撞器合并为一个整体的碰撞器，减小性能消耗。
   ![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-22-09-16.png)
                        *如图*

### 实现相机跟随人物移动
- 法1：写脚本，跟随移动，后面验证
- 法2：简单方法
  - 首先在unity ‘窗口’ ‘包管理器’中导入‘Cinemachine’资源包
        ![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-21-28-45.png)
  - ![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-21-32-03.png)创建2D摄像机，如图。
  - ![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-21-33-43.png)在follow中选择要跟随的对象，这里选择角色即可。
#### 如何实现摄像机不显示背景外面的区域
如果不设置，会出现不太美观的精彩画面，it's excited(doge)
1. 选中你的CM vcam1,在‘Extensions’中选择‘add Extension’中添加"Cinemachine Confiner"(相机边界)
![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-22-25-47.png)
2. 创建空物体对象，随便命名为"CameraConfier" ,为该物体添加可编辑的碰撞器‘Polygon Collider 2D’,
![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-22-31-09.png)
3. 选择合适的点数，修改它的位置，此过程及其生草，可以使用Ctrl 移动鼠标 ，绿边会变红，鼠标点一下就会消失这条边。
4. 相机边界的"Polygon Collider 2D"的“是触发器”勾选上，不然人物会被摄像机的边界挤出去。
5. 另一种解决方案：![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-23-25-09.png)
6. 地图面积还是要方方正正的好，不然限制相机边界会出bug
7. 调整摄像机显示区域大小的方法："Soft Zone Width","Spft Zone Height"  ![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-23-35-08.png)
8. 调整显示区域位置，使角色出现位于左方或者右方的效果，使用"Screen X" "Screen Y"，如图
![d:\Program Files\Unity Project\C# 脚本学习记录](images/2022-03-23-23-40-01.png)
视频推荐：[链接](https://www.bilibili.com/video/BV1r4411d7Zv?spm_id_from=333.337.search-card.all.click)