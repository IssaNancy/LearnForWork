

##### CSS

- (cascading style sheet ,层叠式样式表)是用来给 HTML 标签添加样式的语言
- CSS3 是 CSS 的最新版本,增加了大量的样式、动画、3D 特效和移动端特性等
- 前端三层
  - 结构层 HTML 搭建结构、放置部件、描述语义
  - 样式层 CSS 美化页面、实现布局
  - 行为层 JavaSript 实现交互效果、数据收发、表单验证等

* CSS 使样式和结构分离,样式和结构不用“杂糅着写”, 而是彼此分开:
* HTML 就负责结构, CSS 负责样式 HTML 和 CSS 怎么结合呢? "选择器” 就是两者的纽带
* CSS 的本质
  - CSS 没有加减乘除、与或非、循环、选择、判断，CSS 不是“编程”,就是简单直接的罗列样式
  - 背诵 CSS 属性是非常重要的,属性背诵熟练程度决定了做网页的速度
* CSS 的书写位置
  - 内嵌式：内嵌在 html 文件中,在`<head></head>`标签对中书写`<style></style>`标签对，里面书写 CSS 语句
  - 外链式：将 CSS 单独存为.css 文件，然后用< link>标签引入它
    - `<link rel="stylesheet" href="css/home.css>`
    - `rel:关系 stylesheet：样式表 意思是引入的文件是我的样式表`
    - 优点 多个 html 网页，可以公用一个 css 样式表文件
  - 导入式：最不常见的样式表导入方法`<style>@import url(css/home.css);</style>`
    - 使用导入式引入的样式表，不会等待 css 文件加载完毕，而是会立即渲染 HTML 结构，所以页面会有几秒中的“素面朝天
  * 行内式：样式可以直接通过 style 属性写在标签上
    - `<h2 style="color: red;" >我是一个二级标题</h2>`
    - 行内式牺牲了样式表的批量设置样式的能力，只能给一个标签设置样式，所以不常用
    - 后台工程师经常使用行内式
* CSS3 的基本语法
  - ```css
    h2 {
        color: red;
        /* 背景颜色 */
        background-color: blue;
    }
    
    p {
        color: green;
        /* 背景颜色 */
        background-color: yellow;
    }
    ```

- 标签选择器

  - 标签选择器也称元素选择器、类型选择器，它直接使用元素的标签名当做选择器，将选择页面上**所有该种标签**

  - 标签选择器将选择页面.上所有该种标签，**无论**这个标签所处位置的深浅

  - 标签选择器“覆盖面”非常大，所以通常用于标签的**初始化**

  - ```css
    span {/**span元素是内联元素，可用作文本的容器。**/
    color: red;
    }
    
    b {
    color: green;
    }
    
    ul {
        /* 去掉小圆点 */
        list-style: none;
    }
    a {
        /* 去掉下划线 */
        text-decoration: none;
        color: #333;
    }
    ```

- id选择器

  - 标签可以有id属性，是这个标签的唯一标识

  - id的名称只能由字母、数字、下划线、 短横构成，且不能以数字开头，字母区分大小写，但习惯上一般为小写字母

  - 同一个页面上不能有相同id的标签

    ```css
    <p id="para1">我是一个段落</p>
    ```

  - CSS选择器可以使用#前缀，选择指定id的标签

    ```css
    /*选择id为para1的标签*/
    #para1 {
                color: red;
            }
    ```

- 复合选择器

  - 后代选择器   .box .spec  选择类名为box的标签内部的类名为spec的标签

    **空格表示后代** 后代不一定是儿子

    后代选择器可以有很多空格，隔开好几代

    ```css
    .box p { /*选择类名为box的标签后代的p标签*/
    	color: red;
    }
    
    div.box p.spec em {
        color: red;
    }
    
      /*以下✓将会被选择*/
    <div class="box">
      <p>我是盒子中的段落</p> ✓
      <p>我是盒子中的段落</p> ✓
      <ul>
          <li><p>我是盒子中的段落</p></li> ✓
          <li><p>我是盒子中的段落</p></li> ✓
      </ul>
    </div>
    ```

  - 交集选择器   li.spec  选择既是li标签，也属于spec类的标签

    交集选择器不能有空格

    ```html
    h3.spec {
        font-style: italic;
    }
    
        <div class="box">
          <ul>
            <li>
              <p>我是段落</p>
            </li>
            <li>
              <p class="spec">我是段落<em>强调文字</em></p>
            </li>
          </ul>
        </div>
    
    ```

  - 并集选择器    ul, ol  选择所有ul和ol标签

    ```css
    ul,ol {
        list-style: none;
    }
    
        <ul>
          <li>无序列表的列表项</li>
          <li>无序列表的列表项</li>
          <li>无序列表的列表项</li>
          <li>无序列表的列表项</li>
        </ul>
    
        <ol>
          <li>有序列表的列表项</li>
          <li>有序列表的列表项</li>
          <li>有序列表的列表项</li>
          <li>有序列表的列表项</li>
        </ol>
    ```

- 伪类
  - 伪类是添加到选择器的描述性词语，指定要选择的元素的特殊状态，超级链接拥有4个特殊状态
  - a:link  没有被访问的超级链接
  - a:visited  已经被访问过的超级链接
  - a: hover  正被鼠标悬停的超级链接
  - a: active  正被激活的超级链接(按下按键但是还没有松开按键）
  - 爱恨准则：
    - a标签的伪类书写，要按照"爱恨准则”的顺序，否则会有伪类不生效
    - **L** O **V** E   **H** **A **T E
    - **L**ink   **V**isited   **H**over   **A**ctive

- 元素关系选择器

  - 子选择器            div > p       div的子标签p

    - 当使用 **>** 符号分隔两个元素时，它只会匹配那些作为第一个元素的直接后代元素,即两个标签为父子关系 .box>p{} 和.box p{} 不一样

    - 后代选择器不一定限制是子元素

    - 从IE7开始兼容

      <img src="C:\Users\pc\AppData\Roaming\Typora\typora-user-images\image-20230401193346526.png" alt="image-20230401193346526" style="zoom:80%;" />

  - 相邻兄弟选择器 img + p      图片后面紧跟着的段落将被选中

    - 相邻兄弟选择器(+)介于两个选择器之间，当第二个元素紧跟在第一个元素之后，并且两个元素都是属于同一个父元素的子元素，则第二个元素将被选中

    - a+ b就是选择“ 紧跟在a后面的一个b

    - 从IE7开始兼容

      <img src="C:\Users\pc\AppData\Roaming\Typora\typora-user-images\image-20230401193533528.png" alt="image-20230401193533528" style="zoom:80%;" />

  - 通用兄弟选择器 p ~ span     p元素之后的所有同层级span元素

    - 通用兄弟选择器(~) ，a~b选择a元素之后所有同层级b元素

    - 从IE7开始兼容

      <img src="C:\Users\pc\AppData\Roaming\Typora\typora-user-images\image-20230401193707864.png" alt="image-20230401193707864" style="zoom:80%;" />

-  序号选择器

  - :first-child  第一个子元素

  - :first-child表示"选择第一个子元素”比如下面的例子就表示选择.box1盒子中第一个p

    ```css
    .box1 p:first-child {
        color: red;
    }
    <div class="box1">
        <p>1</p>  ✓
        <p>2</p>
        <p>3</p>
        <p>4</p> 
    </div>
    ```

  - : last- child  最后一个子元素

    ```css
    .box1 p:last-child {
        color: blue;
    }
    <div class="box1">
        <p>1</p>
        <p>2</p>
        <p>3</p>
        <p>4</p>  ✓
    </div>
    ```

  - :nth-child(3)  第3个子元素  2n+1 = odd 表示奇数 2n=even 表示偶数

    ```css
    /*:nth-child()可以选择任意序号的子元素*/
    .box2 p:nth-child(3) {
        color: green;
    }
    
    .box3 p:nth-child(odd) {
        color: orange;
    }
    
    <div class="box2">
        <p>1</p>
        <p>2</p>
        <p>3</p>   ✓
        <p>4</p>
    </div>
    
    <div class="box3">
        <p>1</p>   ✓
        <p>2</p>
        <p>3</p>   ✓
        <p>4</p>
        <p>5</p>   ✓
    </div>
    /*:nth-child()可以写成an+b的形式
      表示从b开始每a个选一个
      不能写成b+an*/
    .box2 p:nth-child(3n+2) {
        color: green;
    }
    <div class="box2">
        <p>1</p>
        <p>2</p>   ✓
        <p>3</p>
        <p>4</p>
        <p>5</p>   ✓
        <p>6</p>
    </div>
    /*若box4中的第3个不是p标签 则失效
      此时，应使用:nth-of-type(3)*/
    .box4 p:nth-child(3) {
        color: green;
    }
    <div class="box4">
        <p>我是1号p</p>
        <p>我是2号p</p>
        <h3>我是1号h3</h3>
        <h3>我是2号h3</h3>
        <p>我是3号p</p>    ×
        <p>我是4号p</p>
        <h3>我是3号h3</h3>
        <h3>我是4号h3</h3>
    </div>
    ```

  - :nth-of-type(3)  第3个某类型子元素

    ```css
    .box4 h3:nth-of-type(3) { /*选择第三个p*/
        color: rgb(136, 50, 79);
    }
    <div class="box4">
        <p>我是1号p</p>
        <p>我是2号p</p>
        <h3>我是1号h3</h3>
        <h3>我是2号h3</h3>
        <p>我是3号p</p>    ✓
        <p>我是4号p</p>
        <h3>我是3号h3</h3>
        <h3>我是4号h3</h3>
    </div>
    ```

  - :nth-last-child(2)  倒数第2个子元素

    ```css
    .box5 p:nth-last-child(2) {/*选择box5中倒数第二个*/
        color: sienna;
    }
    <div class="box5">
        <p>我是1号p</p>
        <p>我是2号p</p>
        <p>我是3号p</p> ✓
        <p>我是4号p</p>
    </div>
    
    .box5 p:nth-last-of-type(2) {/*选择box5中的p中倒数第二个*/
        color: sienna;
    }
    <div class="box5">
        <p>我是1号p</p>
        <p>我是2号p</p>
        <p>我是3号p</p> ✓
    	<h3>我是h3</h3>
        <p>我是4号p</p>
    </div>
    ```

  - 序号选择的兼容性

    - ：first-child                IE7
    - ： last-child                IE9
    - ：nth-child(3)             IE9
    - ：nth-of-type(3)         IE9
    - ：nth-last-child(3)      IE9
    - nth-last-of-type(3)      IE9

-  属性选择器

  - img[alt]                      选择有alt属性的img标签

  - img[alt="故宫"]         选择alt属性是故宫的img标签

  - img[alt^="北京"]       选择alt属性以北京开头的img标签

  - img[alt$=' "夜景"]     选择alt属性以夜景结尾的img标签

  - img[alt*="美"]           选择有alt属性中含有美字的img标签

  - img[alt~="手机拍摄"]  选择有alt属性中有空格隔开的手机拍摄字样的img标签

  - img[alt|="参赛作品"]  选择有alt属性以“参赛作用”开头的img标签

    ```css
    [alt] 有这个属性
    [alt = "北京故宫"] 精确匹配
    [alt ^= "abc"] 开头匹配
    [alt $= "abc"] 结尾匹配
    [alt *= "abc"] 任意位置匹配
    [alt |= "abc"] abc-开头
    [alt ~= "abc"] abc为空格分开的独立部分
    ```

-  css3新增伪类

  - : empty     选择空标签
  - : focus       选择当前获得焦点的表单元素
  - : enabled  选择当前有效的表单元素
  - :disabled  选择当前无效的表单元素
  - : checked  选择当前已经勾选的单选按钮或者复选框
  - : root         选择根元素，即`<html>`标签

-  伪元素

  CSS3新增了"伪元素”特性，顾名思义，表示虚拟动态创建的元素

  伪元素用双冒号表示，IE8可以兼容单冒号

  - ::before创建一个伪元素 ，其将成为匹配选中的元素的第一个子元素，必须设置content 属性表示其中的内容

  - : :after 创建一 个伪元素， 其将成为匹配选中的元素的最后一个子元素，必须设置content属性表示其中的内容.

    ```css
    a::before {/*所有超级链接的文字前都会添加■*/
        content: "■";
    }
    a::after {
        content: "❤";
    }
    ```

    <img src="C:\Users\pc\AppData\Roaming\Typora\typora-user-images\image-20230401211913916.png" alt="image-20230401211913916" style="zoom:50%;" />

  - : :selection CSS伪元素应用于文档中被用户高亮的部分 (使用鼠标圈选的部分)

  ```css
  .box1::selection {
  /* 背景颜色 */
  background-color: springgreen;
  color: deeppink;
  }
  ```

  -  :: first-letter会选中某元素中(必须是块级元素)第一行的第一个字母
  -  ::first- line会选中某元素中(必须是块级元素)第一行全部文字

  ```css
  .box1::first-letter {
  font-size: 50px;
  }
  
  .box1::first-line {
  /* 添加下划线 */
  text-decoration: underline;
  }
  ```

-  层叠性

  CSS全名叫做"层叠式样式表”，层叠性是它很重要的性质

  层叠性:多个选择器可以同时作用于同一个标签，效果叠加

  - 层叠性:多个选择器可以同时作用于同-一个标签,效果叠加

    ```html
    <body>
        <p id="para" class="spec">我是段落</p>
    </body>
    
    <style>
        p {
        color: red;
        }
    
        .spec {
        font-style: italic;
        }
    
        #para {
        text-decoration: underline;
        }
    </style>
    ```

  - 层叠性的冲突处理

    ```html
    <!-- 如果多个选择器定义的属性有冲突呢? CSS有严密的处理冲突的规则 -->
    <!--    id权重> class权重>标签权重    -->
    <style>
        p {
            color: red;
        }
    
        #para {
            color: green;
        }
    
        .spec {
            color: blue;
        }
    </style>
    ```

  - 复杂选择器权重计算

    ```html
    <!--复杂选择器可以通过(id的个数，class的个数， 标签的个数)的形式，计算权重 -->
    <style>
            #box1 #box2 p { /* 权重(2, 0, 1)*/
                color: red;
            }
            #box1 div.box2 #box3 p {/* 权重(2, 1, 2)*/
                color: green;
            }
            .box1 .box2 .box3 p {/* 权重(0, 3, 1)*/
                color: blue;
            }
    </style>
    
    <body>
        <div id="box1" class="box1">
            <div id="box2" class="box2">
                <div id="box3" class="box3">
                    <p>我是段落</p>
                </div>
            </div>
        </div>
    
        <ul class="list">
            <li>列表项</li>
            <li class="spec">列表项</li>
            <li class="spec">列表项</li>
            <li>列表项</li>
            <li>列表项</li>
            <li>列表项</li>
            <li>列表项</li>
        </ul>
    </body>
    ```

  - !important提升权重

    如果我们需要将某个选择器的某条属性提升权重，可以在属性后面写! important

    ```html
    <style>
    		.list li {/* 权重(0, 1, 1)*/
                color: red;
            }
            .spec {/* 权重(0, 1, 0)*/
                color: blue !important;
            }
    </style>
    <!--很多公司不允许使用!important,因为这会带来不经意的样式冲突-->
    ```

-  文本与字体属性

  常用文本样式属性

  - color属性
    - color属性可设置文本内容的前景色
    - color属性主要可以用英语单词、十六进制、rgb(）、 rgba()等表示法
    - 英语单词表示法，比如`color: red; `仅仅用于学习时临时设置一下颜色，工作时基本不用这样的形式，因为追求精确
    - 十六进制表示法是所有设计软件中都通用的颜色表示法，设计师给我们的设计图上面标注的颜色，通常为十六进制表示`color:#ff0000 ;`
    - 比如十六进制ff就是十进制的255,每种颜色分量都是0~255的数字
    - 如果颜色值是#aabbcc的形式，可以简写为#abc
    - 黑色是#000，白色是#fff,常见的灰色有#ccc、#333、#2f2f2f等
    - 颜色也可以用rgb( )表示法`color: rgb( 255,0,0);`
    - 颜色也可以用rgba()表示法，最后-个参数表示透明度,介于0到1之间，0表示纯透明，1表示纯实心`color: rgba(255, 0, 0, .65);`
    - rgba( )表示法从IE9开始兼容
  - font-size属性用来设置字号，单位通常为px。今后课程上老师还会个绍em、rem单位。`font-size: 30px;`
    - 网页文字正文字号通常是16px，浏览器最小支持10px字号
  - font-weight属性设置字体的粗细程度，通常就用normal和bold两个值
    - `font-weight: normal ;`    正常粗细，与400等值
    - `font-weight: bold;   `     加粗，与700等值
    - `font-weight: lighter ; `   更细，大多数中文字体不支持
    - `font-weight: bolder; `    更粗，大多数中文字体不支持
  - font-style属性设置字体的倾斜
    - `font-style: normal; `  取消倾斜，比如可以把天生倾斜的i、em等标签设置为不倾斜
    - `font-style: italic;   `    设置为倾斜字体(常用)
    - `font-style: oblique;  ` 设置为倾斜字体(用常规字体模拟，不常用)
  - text-decoration属性用于设置文本的修饰线外观的（下划线 删除线）
    - `text-decoration: none; ` 没有修饰线
    - `text-decoration: underline;`  下划线
    - `text-decoration: line- through;`  删除线

- 字体属性

  - font-family属性用于设置字体

    - 字体可以是列表形式，一般英语字体放到前面，后面的字体是前面的字体的"后备”字体
      `font- family: serif, "Times New Roman"， "微软雅黑" ;`

    - 字体名称中有空格，必须用引号包裹

    - 中文字体也可以称呼它们的英语名字

    - font -family: "微软雅黑"  font -family: "Microsoft Yahei"

    - font- family: "宋体"  font -family: "SimSun

    - 字体通常必须是用户计算机中已经安装好的字体,所以一般来说设置为微软雅黑和宋体较多,设置成其他字体较少

    - 如何设置为用户电脑中没有的字体呢?那就必须自己定义新字体，这就需要我们有字体文件，用户加载网页的时候，会同时下载这些字体文件

    - 字体文件根据操作系统和浏览器不同，有eot、 woff2、woff、ttf、 svg文件格式，需要同时有这5种文件

    - 当我们拥有字体文件之后，就可以用@font -face定义字体

      ```HTML
       <style>
       	@font-face {
                  font-family: 'webfont';
                  font-display: swap;
                  src: url('fonts/webfont.eot');
                  /* IE9*/
                  src: url('fonts/webfont.eot') format('embedded-opentype'),
                      /* IE6-IE8 */
                      url('fonts/webfont.woff2') format('woff2'),
                      url('fonts/webfont.woff') format('woff'),
                      /* chrome、firefox */
                      url('fonts/webfont.ttf') format('truetype'),
                      /* chrome、firefox、opera、Safari, Android, iOS 4.2+*/
                      url('fonts/webfont.svg') format('svg');
                  /* iOS 4.1- */
              }
      </style>
      ```

      阿里巴巴提供了一套免费商用授权的普惠字体，使用该字体也省去了下载字体的麻烦
      https://www.iconfont.cn/webfont

      浏览器默认字体：微软雅黑字体

      设置字体时英文字体在前，若中文字体在前会使英文字体失效

      ![image-20230403105842391](C:\Users\pc\AppData\Roaming\Typora\typora-user-images\image-20230403105842391.png)

-  段落和行相关属性

  - text-indent属性定义 **首行文本内容之前的缩进量**

    - 缩进两个字符应该写作`text- indent: 2em;`em表示字符宽度

  - line-height属性 用于定义**行高**

    <img src="C:\Users\pc\AppData\Roaming\Typora\typora-user-images\image-20230403114435627.png" alt="image-20230403114435627" style="zoom:80%;" />

    - line -heigh属性的单位可以是以px为单位的数值`line- height: 30px;`
    - line -heigh属性也可以是没有单位的数值，表示字号的倍数 这是最**推荐**的写法
      `line-height: 1.5;`
    - line-heigh属性也可以是百分数，表示字号的倍数`line-height: 150%;`

  - text-align属性

    - 设置行高=盒子高度，即可实现单行文本垂直居中
    - 设置`text-align: center; `即可实现文本水平居中
    - <img src="C:\Users\pc\AppData\Roaming\Typora\typora-user-images\image-20230403114951242.png" alt="image-20230403114951242" style="zoom:50%;" />

  - font合写属性

    - font可以作为font-style,font-weight ,font-size, line-height和font -family属性的合写
    - <img src="C:\Users\pc\AppData\Roaming\Typora\typora-user-images\image-20230403115425375.png" alt="image-20230403115425375" style="zoom:80%;" />

  - 继承性

    - 文本相关的属性普遍具有继承性，只需要给祖先标签设置,即可在后代所有标签中生效
      color、font-开头的、list-开头的、text-开头的、line-开头的
    - 因为文字相关属性有继承性，所以通常会设置body标签的字号、颜色、行高等，这样就能当做整个网页的默认样式了
    - 就近原则：在继承的情况下，选择器权重计算失效，而是“就近原则”
    - 直接选择>继承     都是继承 看谁更近 一样近 就数个数

-  盒模型

  所有HTML标签都可以看成矩形盒子，由width、 height、padding、border构成

  <img src="C:\Users\pc\AppData\Roaming\Typora\typora-user-images\image-20230403121153535.png" alt="image-20230403121153535" style="zoom:80%;" />

  width、height坏是盒子总宽高。

  盒子的总宽度= width +左右padding +左右border

  盒子的总高度= height +上下padding +上下border

  - width  盒子内容的宽度
    - width属性的单位通常是px，移动端开发也会涉及百分数、rem等单位
    - 当块级元素(div，h系列，li等) 没有设置width属性时，它将自动撑满，但这并不意味着width可以继承
  - height属性 表示盒子内容的高度
    - height属性的单位通常是px，移动端开发也会涉及百分数、rem等单位
    - 盒子的height属性如果不设置，它将自动被其内容撑开，若没有内容，则height默认0
  - padding属性 盒子的内边距，即盒子边框内壁到文字的距离
    - 四个方向：
      - padding-top          上padding
      - padding-right        右padding
      - padding- bottom  下padding
      - padding- left          左padding
    - 四数值写法：
      - padding属性如果用四个数值以空格隔开进行设置，分别表示上、右、下、左的padding： `padding: 10px 20px 30px 40px; `
    - 三数值写法：
      - padding属性如果用三个数值以空格隔开进行设置，分别表示上、左右、下的padding： `padding: 10px 20px 30px;`
    - 二数值写法：
      - padding属性如果用二个数值以空格隔开进行设置，分别表示上下、左右的padding : `padding: 10px 20px;`
    - 灵活设置padding属性 
      - 上下为30px 左右为0 ：`    padding:30px 0; `
      - 上左右为40px 下为0：`padding:40px;padding-bottom:0;` 小属性层叠大属性

  - margin   盒子的外边距，即盒子和其他盒子之间的距离

    <img src="C:\Users\pc\AppData\Roaming\Typora\typora-user-images\image-20230404114316086.png" alt="image-20230404114316086" style="zoom: 67%;" />

    四个方向：

    - margin-top   上margin,        "向 上踹”
    - margin-right 右margin,        "向右踹”
    - margin- bottom 下margin,  "向下踹"
    - margin-left 左margin,           "向左踹”

    margin的塌陷

    - 竖直方向的margin有塌陷现象:小的margin会塌陷到大的margin中，从而margin不叠加，只以**大值**为准

      <img src="C:\Users\pc\AppData\Roaming\Typora\typora-user-images\image-20230404114638582.png" alt="image-20230404114638582" style="zoom:80%;" />

      盒子div元素 默认竖直排列 ；span默认横排列

    - 默认的margin

      一些些元素(body、ul、 p等)都有默认的margin,在制作网页的时候，要将他们清除

      ```css
      * {
      	margin:0;
          padding:0;
      }
      * 是通配符选择器 表示选择所有元素 但是通配符有效率问题，应该使用并集选择器
      
      body,ul,p {
          margin:0;
          padding:0;
      }
      ```

    - 盒子的水平居中

      将盒子左右两边的margin都设置为auto,盒子将水平居中

      ```css
      .box {
          /* 盒子水平居中 */
          margin: 0 auto; /** 上下是0，左右自动**/
          /* 文字居中 */
          text-align: center;
          /* 行高等于盒子高，让文字垂直居中 */
          line-height: 100px;
      }
      ```

      文本居中是text- align: center; 和盒子水平居中是两个概念
      盒子的垂直居中，需要使用绝对定位技术实现

  - 盒模型计算

    <img src="C:\Users\pc\AppData\Roaming\Typora\typora-user-images\image-20230405085109520.png" alt="image-20230405085109520" style="zoom:80%;" />

  - box-sizing属性

    将盒子添加了box-sizing: border-box;之后，盒子的width、height数字就表示盒子实际占有的宽高(不含margin)了，即padding、 border变为 "内缩”的，不再“外扩"

    ```css
    <style>
        .box {
            box-sizing: border-box;
            width: 200px;
            height: 200px;
            border: 10px solid #000;
            padding: 10px;
        }
    </style>
    ```

    box-sizing属性大量应用于移动网页制作中，因为它结合百分比布局、弹性布局等非常好用，在PC页面开发中使用较少，box-sizing属性兼容到IE9

  - display属性

    - 行内元素和块级元素

    | display属性类型 | 是否能并排显示 | 是否能设置宽高 | 当不设置width属性时 | 举例                                   |
    | --------------- | -------------- | -------------- | ------------------- | -------------------------------------- |
    | 块级元素        | 否             | 是             | width自动撑满       | div、section、 header、h系列、li、ul等 |
    | 行内元素        | 是             | 否             | width自动收缩       | a、span、 em、b、u、i等                |

    - 行内块

      img和表单元素是特殊的行内块，它们既能够设置宽度高度也能够并排显示

  - 行内元素和块级元素的相互转换

    - 使用`display: block ;`即可将元素转为块级元素

    - 使用`display:inline;`即可将元素转为行内元素，将元素转为行内元素的应用不多见
    - 使用`display: inline- block ;`即可将元素转为行内块

  - 元素的隐藏(用于特效)

    - 使用`display: none ;`可以将元素隐藏，元素将彻底放弃位置，如同没有写它的标签一样 。

    - 使用`visibility: hidden;` 可以也可以将元素隐藏，但是元素不放弃自己的位置

  



