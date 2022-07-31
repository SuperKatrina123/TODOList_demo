### 设计需求

题目来源：字节校招题_[todoList设计](https://www.nowcoder.com/question/next?pid=8537237&qid=141038&tid=58964111)

设计一个TODO List，页面结构如下图所示，要求：

1. 使用HTML与CSS完成界面开发
2. 实现添加功能：输入框中可输入任意字符，按回车后将输入字符串添加到下方列表的最后，并清空输入框
3. 实现删除功能：点击列表项后面的“X”号，可以删除该项
4. 实现模糊匹配：在输入框中输入字符后，将当前输入字符串与已添加的列表项进行模糊匹配，将匹配到的结果显示在输入框下方。如匹配不到任何列表项，列表显示空

**注：以上代码实现需要能在浏览器中正常显示与执行。**

![img](https://uploadfiles.nowcoder.com/images/20170905/300557_1504600345720_0731F532C5041A67ADDD38896EFDC6DD)

### 实现思路

#### （1）UI部分

- title：h1
- 输入框：input
- list展示：ul li
- 向下箭头和叉叉：[阿里图标矢量库](https://www.iconfont.cn/)

CSS自己魔改就行~

可以增加一些小细节，比如hover到input框的时候显示input的边框等~

#### （2）操作部分

- keydown监听——在input框输入，按下回车键后，动态显示
  - input输入——输入内容可以由input.value获取
  - 按下回车键后——回车键的keycode为13
  - 动态显示——动态创建li并为li添加显示value的span和显示叉叉的span作为子节点，最后li作为子节点插入到ul中
- keyup监听——模糊搜索
  - 通过监听keyup事件，获取input.value
  - 获取所有的显示value的span，遍历其内容（spanValue），判断spanValue中是否包含value（通过indexOf判断）
  - 如果包含，则利用正则表达式，把符合的部分替换成红色字体
- onclick监听——如果点击叉叉则删除内容
  - 实际上是删除li
  - 需要找到onclick绑定事件的元素，找到其父元素，并通过父元素的父元素（parentNode）删除子节点即可
  - 在这个案例里面，则是找到显示叉叉的span的li节点，并且通过ul删除li即可（removeChildNode）

### 知识点

- 事件监听
  - 可监听的事件
  - event.target指向被监听的元素
- 获取value
  - input.value
  - 标签.innerText和innerHTML的区别
- DOM
  - 获取元素的方式：getElementById getElementsByClassName ...
  - 动态创建节点：createElement(标签)
  - 添加元素属性：setAttribute('calss'， ’box‘)
  - dom节点属性：parentNode childNodes
  - 元素classList属性【HTML新增】:看这篇：[DOM | classList属性](https://superkatrina123.github.io/2022/07/29/HTML/DOM_classList属性/)
  - ...

### 实现效果

![img](https://superkatrina123.github.io/2022/07/31/Demo/todoList/todoList_%E8%AE%BE%E8%AE%A1todoList/%E6%95%88%E6%9E%9C.png)

### Code

[todoList_demo](https://github.com/SuperKatrina123/TODOList_demo)
