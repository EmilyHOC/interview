### 3.1 CSS3
    * 面试题
* 什么是CSS预处理器
> CSS预处理器就是为CSS增加编程特性，通过编译器将新语法的文件输出为普通的CSS文件
        > 常见的预处理器：Less,Sass,Stylus
        
* CSS预处理器的优缺点：
    ##### 优点：
    > 变量存储多次引用的信息

    > minxin能够重用一段样式代码
        
    > 内置丰富的函数
        
    > 可以嵌套选择器
        
    > 使用数学运算
        
    ##### 缺点：
    > 调试难度增加

    > 降低对CSS文件的控制能力
    
    > 学习成本
    
### 3.2 盒模型
* 1.W3C盒模型包含内容：margin,border,padding,content
    IE盒模型包含内容：content包含padding和border
    代码：/public/3.2test.html(已知父元素宽高上下左右居中)
* 2.更改盒模型的属性：
    content-box:对应W3C盒模型
    border-box对应IE盒模型
* 3.盒子的显示类型
    block,inline-block,inline-block,table,flexbox
* 4.面试题：
    > 什么是外边距坍塌?
    * 也称为外边距合并，是指在两个正常流中相邻的块级元素的外边距组合变成单个边距
    ，只有上下边距会坍塌，左右不会

    坍塌的情况：
    * 父元素没有边框和上内边距，和第一个子元素
        代码：/public/3.2test2.html
    * 父元素没有下边框和下内边距
         代码：/public/3.2test3.html
    * 两个相邻兄弟元素，分别定义了下边距和上边距
         代码：/public/3.2test4.html
    * 一个空的元素，只定义了上下外边距
        代码：/public/3.2test5.html
    > 当出现外边距坍塌计算方式？
    * 两正取大，两负取绝对值大，一正一负取相加和

### 3.3盒类型
* list-item
    指定元素为列表，相当于变成了li
    代码：/public/3.3test1.html
    
* table(不提倡)

* run-in根据周围元素决定盒子类型（兼容问题）

* inline-block
    * 让元素排列在一行
    * 会有间隙问题：解决办法
    * 三个子元素写在一行
    * 父元素letter-spacing为负，子元素letter-spaceing为0
    * 父元素font-size:0(没效果不知道为啥)
    * 代码：代码：/public/3.3test1.html
            
* flexbox
    * 不会有间隙问题
        > 父元素：display:flex

       >子元素：flex:占几份
*
        面试题：
        display:none和visibility:hidden都可以隐藏元素,两者有什么区别
        将CSS属性display定义为none后，相当于元素没有了后代元素，在正常流中不占用任何空间，元素真实的尺寸
        将会丢失，还会导致浏览器重排和重绘，visibility:hidden在正常流还会占据空间，仍具有真实尺寸
        ，只会导致重绘
        
### 3.4 BFC
*(BFC有隔离作用，内部元素不受外部影响，BFC内容不会与外面浮动元素重叠)
* 1.创建BFC
    * (1)根元素，也就是HTML元素
    * (2)float属性不为none的浮动元素
    * (3)position属性是absolute或fixed的定位元素
    * (4)display属性为inline-block,table-cell或伸缩盒模型
    * (5)overflow属性不为visible的块级元素
* 2.BFC的用途
* 
        (1)清除浮动
            当一个元素定义浮动，附近文字环绕，解决办法：浮动的父元素清浮动
            代码：/public/3.4test1.html
            一个父元素未定义高度，有浮动的子元素,高度坍塌，解决办法父元素清浮动
            代码：/public/3.4test2.html

*       (2)解决外边距坍塌
            代码：/public/3.4test3.html
*       (3)宽度自适应的两栏布局
            左边宽度固定，右边清除浮动后可以自适应两栏布局
            代码： 代码：/public/3.4test4.html
            
### 3.5 CSS选择器
        1.基本选择器
            通配选择器
            类型选择器
            类选择器
            ID选择器
            属性选择器
        2.关系选择器
            后代选择器
            子选择器（.bfc>ul）只会选择儿子，缩小范围
            相邻选择器和兄弟选择器
            .bfc+div{} //相邻选择器
            .bfc~div{}//兄弟选择器 
            案例代码：/public/3.5test1.html           
        3.伪选择器
            (1)伪类选择器：用于描述元素的动态特征，再根据元素的特殊状态选择元素
                *链接元素
                未访问(:link)已访问(:visited)激活(:active)悬停(:hover)
                *元素的位置
                第一个(:first-child)
                *表单元素
                选中(:checked)启用(:enabled)禁用(:disabled)
            (2)伪元素选择器
                用于处理文档内容或添加内容或过滤内容
                过滤内容：::first-letter(首字符)::selection(选中内容)
                添加内容：::before(元素之前插入内容) ::after(元素之后插入内容)
             注意:伪元素只能出现在选择器的最后位置，并且不能同时定义多个伪元素
        4.面试题
        伪类：first-child与：first-of-type有什么区别
            伪类:first-child表示父元素中的第一个子元素，只要这个元素在第一位置就能够匹配
            伪类:first-of-type表示父元素中的第一个与父元素相同类型的子元素
             代码：/public/3.5test2.html

### 3.6 内容生成
        content属性可以用来生成内容，创建计数器，引用属性值和图像
             (1)生成内容
                 代码：/public/3.6test1.html     
             (2)属性值
                在content属性中应用attr()函数 
                代码：/public/3.6test2.html(不要在chrome中打开)
                
### 3.7 层叠
        面试：
        链接的四种状态声明的顺序：
        推荐使用的顺序是：LVHA（:link,:visited,:hover,:active）love,hate记忆
### 3.8 单位
        1.em：表示的是元素字体大小的倍数
        换算公式：1/元素的font-size*px
        2.rem:和em大小相关，参照的是根元素字体的大小
         换算公式：1/htmlfont-size*px
        面试题：用过calc()函数吗？是什么有什么作用？
        calc()是CSS的一个函数，用来处理数学运算并且混用单位，如果用百分比做自适应布局的时候会用到
        代码：/public/3.8test1.html
        
### 3.9 百分数
        1）定位：
        fixed包含块是当前视口
        absolute包含块是离他最近祖先元素不为static的内容区域
        面试题：
        执行下面代码计算后p元素的行高是多少
        ```
        div{
            font-size:18px;
            line-height:14px;
        }
        div p{
            line-height:50%;
        }
        行高参照的是元素自身的字体大小，p元素自身并没有定义字体，需要从父元素继承来，继承过来的
        值是18px再乘以50%，最终行高是9px
        代码：/public/3.9test1.html
        
### 3.10 颜色
    * 
    面试题：
        在CSS使用background:transparent与opacity:0区别
        在CSS中，transparent关键字相当于rgba(0,0,0,0),作为background的属性值
        仅仅是将元素的背景设为透明，元素中的内容还能显示，而opacity:0是把元素和内容当成一个整体，两者都会
        透明
    代码：/public/3.10test1.html
                