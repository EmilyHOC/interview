### 5.1布局
* 浮动布局：文档的内容按照一定的规则排列
* 定位布局：不规则的排版，用z-index改变层叠的顺序
* 流式布局：用百分数表示宽高，可以很好地自适应
* 弹性布局：多应用与移动端，弹性布局参照的是字体的大小,使用rem单位参照根元素html
* 多列布局
* 等高布局
* 面试题：如何实现一个圣杯布局？
> 答案：圣杯布局是指页面从上到下由页头，内容和页脚组成，内容由左中右三列组成(code:/public/5.1test1.html)
 * 如图：
![](https://user-gold-cdn.xitu.io/2019/1/3/1681259aeb7ae66d?w=856&h=632&f=png&s=11125)

### 5.2 CSS Reset
* 面试题：
> Reset.css和Normalize.css由什么区别
* 两者的理念不一样,reset.css统一初始外观，nomalize.css统一元素的表现形式
* reset.css牺牲元素的默认样式，normailize.css保留元素的默认样式
* normalize.css修复浏览器的Bug,reset.css没有这个功能

### 5.3伸缩盒布局
关键字：
* flex-direction(创建主轴)
* flex：创建伸缩容器
* justify-content:主轴对齐
* align-items:侧轴对齐
* flex-wrap:控制子元素换行
> 面试题：移动端使用伸缩盒内只显示一行文本，溢出内容省略号替换？(code:/public/5.3test1.html)
```
 div{
            width:200px;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }
```
### 5.4居中
* 水平居中
    * 先将定位元素从包含块的左边界向右偏移50%的距离，再反向偏移一半元素宽度的距离(父容器relative,子容器absolute
![](https://user-gold-cdn.xitu.io/2019/1/3/168127958b49934c?w=375&h=344&f=png&s=4524)
    * 如果定位的元素宽度未知，就不能用外边距，需要用位移属性
    
![](https://user-gold-cdn.xitu.io/2019/1/3/168127edb0b4f591?w=174&h=174&f=png&s=2471)
```
 .container{
            width:100px;
            height:100px;
            border: 1px solid #00CCFF;
            position: absolute;
        }
        .small{
            border: 1px solid #FFCC00;
            position: absolute;
            left:50%;
           transform:translateX(-50%);
        }
<div class="container">
    <div class="small">居中啊兄弟</div>
</div>
```
* 伸缩盒(子元素的高度自动等于容器的高度并且不兼容IE)
```
        .main{
            display: flex;
            justify-content: center;
            border: 1px solid #00CCFF;
            width:200px;
            height: 200px;
        }
    <div class="main">
        <div class="small">居中听到没有</div>
    </div>
```
![](https://user-gold-cdn.xitu.io/2019/1/3/16812962ed3405a7?w=376&h=282&f=png&s=7869)

* 垂直居中
 * 定位：同水平居中一样
 * 伸缩盒：```display:flex;align-items:center```
