# 我永远向往着创造奇迹的人
## 任务目标
游戏大体框架，素材动画不用搞用别的代替，先让小人能跑能跳能打怪开背包掉血

### 待解决的技术问题
- 背包打开过程中的脚本，我打开一个背包，要能看到里面的物品数量，以及我能做出选择。
- 摄像头调整镜头为侧视图那种，不是俯视图。
- 实现使用普通的图片，拼凑地图
- 尝试使用物品小标志当做自主设置怪物的练习，并赋予脚本，属性，触发器 

今晚先把之前的代码搞定，后面再找个2d游戏做做
## 功能需求
wasd  上下左右移动
space 空格跳跃

## 研读代码

移动代码部分
```c#
//======移动==============
        float moveX = Input.GetAxisRaw("Horizontal");//控制水平移动方向，A:-1 D:1
        float moveY = Input.GetAxisRaw("Vertical");//控制垂直方向  W:1 S:-1 不按:0
        //以上，使用方向键上下左右也是一样的
        Vector2 moveVector = new Vector2(moveX, moveY);
        Vector2 position = rbody.position;
        position += moveVector * speed * Time.deltaTime;
        rbody.MovePosition(position);
```