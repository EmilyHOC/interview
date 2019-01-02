### 4.1 浮动
* 创建BFC
  * bfc之间不会重叠，更不会覆盖(代码：/public/4.1test1)
* 清除浮动
  * 浮动元素的缺陷是包含块高度坍塌，也就是浮动元素不能把包含块撑起来，另外就是影响兄弟元素
  * 方法一：包含块用BFC包裹即overflow:hidden
  * 方法二：clear属性，会增加元素的上外边距
  #### 面试题：
```
 div{
        float: left;
        width:80px;
        height: 80px;
        background-color: #FFCC00;
    }
    P{
        clear: both;
        margin-top: 15px;
    }
    <section >
        <div></div>
        <p >已设置上外边距</p>
    </section>
```
![](https://user-gold-cdn.xitu.io/2019/1/2/1680dfab41399c57?w=310&h=252&f=png&s=5175)
> 虽然定义了15px的上外边距，但是为什么失效了

>答案：浮动元素会脱离正常的文档流，clear属性会让元素增加上外边距,使其在浮动元素的下面。在上面的代码中，浮动元素的高度是80px，所以clear属性会给p元素增加80px的上外边距，比定义的15px要大，因此最终的上外边距是80px，正好在浮动元素的下面

### 4.2定位
* 相对定位
不会脱离正常流，也不会改变元素的盒类型。相对定位会根据原先的位置偏移，并且原先所占的空间还会保留
* 绝对定位会脱离正常流，并且会将元素变成块级元素，元素在被设为绝对定位后，其原先所占空间会被删除，并且相对于包含块偏移，它的包含块就是离他最近的position不为static的祖先元素的内容区域。
* 固定定位，包含块是当前视口，即使给父元素设置超出部分隐藏固定定位的元素也不会被裁剪
* z-index改变元素的层叠位置，越大越不容易覆盖
### 4.3边框
> 面试题
```
下面关于border:none以及border:0的区别错误的是(C,D)
A.当border为none的时候，边框无外观
B.当border为0的时候，边框宽度为0
C.当border为none的时候，边框宽度为0
D.只要定义了边框宽度，就能显示边框
  div{
      border:none;
      /*等效于*/
      border-width:medium;
      border-style:none;
      border-color:前景色
  }
  div{
      border:0;
      /*等效于*/
      border-width:0;
      border-style:none;
      border-color:前景色
  }
  ```
  ### 4.4文本属性
  * overflow:visible|hidden|scroll|auto
  * text-decoration
  * white-space
  * 文本换行：word-wrap|word-break
  * 面试题
>如何用纯CSS的方式让超出容器宽度的文本自动替换为省略号？
```
可以使用text-overflow属性，这个属性用于显示内容溢出时的省略标记，但要实现这个效果需要满足三个条件：容器要有明确的宽度，强制在一行显示以及隐藏溢出的内容
```
```
 p{
    width: 200px;/*容器宽度*/
    white-space:nowrap;/*强制在一行*/
    overflow: hidden;/*隐藏溢出*/
    text-overflow: ellipsis;/*省略号*/
}
```
另外溢出部分的选择属性：clip(截断),ellipsis(三点省略)
### 4.6垂直对齐
* line-height主要影响的是行内元素而不是块级元素
* 行内元素分为替换和非替换元素，替换元素是指内容需要外部引入或用户写入的元素如input,img,vedio
* vertical-align:baseline(父元素的基线)|top(行内盒顶端)|bottom|middle
* 注意：当给子元素设置vertical-align属性的时候父元素的基线会被下移(代码：/public/4.6test1.html)
### 4.7背景
* 背景图像尺寸
 * background-size:contain(保持宽高比缩放进内容区)|cover(原图像缩放覆盖背景区)代码：/public/4.7test2.html
* 背景图像定位
 *background-position:10px 20px
### 4.8变形过渡和动画
* 变形函数：transform属性的值是一个变形函数
 * tanslate()位移函数，第一个是水平偏移的值，第二个是垂直偏移的值
 * scale() 缩放函数
 * skew() 倾斜函数
 * rotate()旋转函数
* 过渡属性
 * transition:属性名(all,所有属性都会执行过渡)，持续时间，延迟时间，缓动函数
 * 触发条件CSS伪类，媒体查询和JavaScript