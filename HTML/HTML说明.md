###### vscode 设置

更改颜色主题：文件 首选项 颜色主题 light+default light
ctrl + 滚轮：设置中 勾选 Editor：Mouse Wheel Zoom
vscode 打开 html 页面
Sublime 快捷键扩展：安装 Sublime Text Keymap and Settings Importer

- ctrl shift d 复制当前行
- ctrl shift 上箭头 上移当前行
- ctrl shift 下箭头 下移当前行
  多行编辑： 按住滚轮往下拉

##### HTML

html ：HyperText Mark-up Language 超文本标记语言 超文本标记=标签 文件是纯文本的
Live Server 插件(网页必须存放在文件夹中，且 vscode 已打开这个文件夹) 只支持 UTF-8 字符集 不支持 gb2312

- 自动刷新网页
- 在 html 文件中，按 ctrl + shift + p 键，选择"Open with Live Server"
  W3C 1994 年 美国 是万维网的主要国际标准组织 负责制定 web 标准，主要是 html 和 css

##### HTML5 骨架说明

```html
<!DOCTYPE html> 文档类型说明DTD，必须写 不写DTD会引发浏览器的一些兼容问题
<html lang="en">
  lang属性表示网页的语言，zh表示中文
  <head>
    网页的配置
    <meta charset="UTF-8" />
    meta： 元标签 表示网页的基础配置 charset：字符集设置
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    用户真正能看见的内容 Hello 你好
  </body>
</html>
```

##### 标签

- 单标签 html4 结尾必须短斜杠 html5 不用

  - meta

- 标题标签
  - h 系列 h1-h6 重点内容放到 h1 中 只能有一个和 h1 标签
  * h 系列 添加 id 属性 称为页面的锚点 网址后加# 页面将自动滚动到锚点所在的位置
    - ```html
      <h1 id="cq">重庆美景</h1>
      ```
    - 其他页面的超级链接 可以链接到指定锚点
    - ```html
      <a href="旅游.html#cq">看重庆美景</a>
      ```
- 段落标签

  - p 任何段落都要放到 p 标签中 不能嵌套其他 h 系列标签和其他 p 标签

* title
  - 用来设置网页的标题，文字会显示在浏览器的标签栏上
* meta
  - 设置网页关键词和描述
  - name 属性 设置 meta 的具体功能
  - content 属性 网页的内容

- div -class 分隔标签 盒子
  - 分割，将相关的内容组合在一起，以和其他内容分割，是文档结构更加清晰
  - 可以结合 css 使用 实现网页的布局
  - 习惯性称为盒子
  * 常见类名 添加 class 属性 类名服务于 css
    - 页头 header
    - logo logo
    - 导航条 nav
    - 横幅 banner
    - 内容区域 content
    - 页脚 footer

* img 图片标签

  - 在网页中插入图片 图片必须要复制到项目文件夹中，一般保存在项目文件夹中的 images 子文件夹中

  * alt 属性 对图像文本的描述 不是强制性的，若由于某种原因无法加载图像，浏览器上在页面上显示 alt 属性的备用文本
  * alt 属性供视力不方便的人使用浏览器，也会朗读 alt 中的内容
  * width、height 属性 设置宽度和高度 单位是像素 但不需要写单位，若省略一个属性，则按原始比例缩放图片
  * 支持的图片格式
    - bmp windows 画图软件默认保存的格式 位图
    - gif 支持动画 如表情包
    - jpeg、jpg 有损压缩图片 用于照片
    - png 便携式网络图片 用于 logo 背景图形 支持透明和半透明
    - svg 矢量图片
    - webp 最新的压缩算法 非常优秀的图片格式
  * 相对路径 从网页出发 如何找到图片 ../ 回退一级
  * 绝对路径 图片的精准位置 /
  * 网页超级链接 将网页和网页连接到一起的方法
    - a 标签
      - href 属性支持相对和绝对路径 指向具体的网页
      - title 属性 设置鼠标的悬停文本
      - target 属性 设置为 blank：在新标签中打开网页
  * 图片超级链接

    - a 标签中包裹 img 标签

  * 下载链接
    - 指向 exe zip rar 等文件格式的链接，将自动称为下载链接
    - ```html
      <a href="1.zip">下载</a>
      ```
  * 邮箱链接
    - 有 mailto：前缀的链接是邮箱链接，系统将自动打开 Email 相关软件
    - ```html
      <a href="mailto:23535270492qq.com">给我发邮件</a>
      ```
  * 电话链接
    - 有 tel：前缀的链接是电话链接，系统将自动打开拨号盘
    - ```html
      <a href="tel:12306">打电话买火车票</a>
      ```

  ```html
  <img src="images/img.jpg"
  ```

* audio 音频标签

  - 兼容到 IE9
  - ```html
    <!--controls 显示播放控件
        autoplay 自动播放 一般为不打扰用户 不使用
        loop 循环播放
        src=音频地址
        标签中的文字是对不兼容留恋的显示文字  -->
    <audio controls src="音频地址" autoplay loop>
      抱歉，您的浏览器不支持audio标签，请升级浏览器
    </audio>
    ```

* video 视频标签

  - 兼容到 IE9

  * ```html
    <!--controls 显示播放控件
        autoplay 自动播放 一般为不打扰用户 不使用
        loop 循环播放
        src=视频地址
        标签中的文字是对不兼容留恋的显示文字  -->
    <audio controls src="视频地址" autoplay loop width="300">
      抱歉，您的浏览器不支持video标签，请升级浏览器
    </audio>
    ```

* html5 大纲区块标签
  - section 文档的区域 语义比 div 大
  - article 文档的核心文章内容， 会被搜索引擎主要抓取
  - aside 文档的非必要内容 比如广告等
  - nav 导航条
  - header 页头
  - main 网页核心部分
  - footer 页脚
* span 标签
  - 文本中的区块标签 本身没有特殊的显示效果 结合 css 来丰富样式
  * ```html
    <p><span>北京</span>的区号是<span>010</span></p>
    <p><span>上海</span>的区号是<span>021</span></p>
    ```
* b u i 语义标签
  - 已经被 css 替代
  - b：加粗 u：下划线 i：倾斜
  * ```html
    <p>
      <b>慕课网</b>
      <u>慕课网</u>
      <i>慕课网</i>
    </p>
    ```
* strong em mark 语义强调标签
  - strong: 特别重要文字
  - em ：强调文字
  - mark ：高亮文字
  * ```html
    <p>我<strong>一定</strong>好好学习</p>
    <p>我<em>一定</em>好好学习</p>
    <p>我<mark>一定</mark>好好学习</p>
    ```
* figure figcaption 标签

  - figure 元素 代表一段独立的内容 与 figcaption 配合使用 是一个独立的引用单元
  - ```html
    <p>
      北京是一个美丽的城市。北京是一个美丽的城市。北京是一个美丽的城市。北京是一个美丽的城市。北京是一个美丽的城市。北京是一个美丽的城市。
    </p>
    <p>
      <figure>
        <img src="images/beijing/1.jpg" alt="" />
        <figcaption>北京鸟巢</figcaption>
      </figure>
      <figure>
        <img src="images/beijing/2.jpg" alt="" />
        <figcaption>颐和园十七孔桥</figcaption>
      </figure>
    </p>
    ```

* 表单

  - 收集信息 如 登陆 注册 发送评论反馈 购买商品等

  - 表单的创建

    - 表单以 form 元素开始
    <!-- action:表单要提交的后台程序的网址
         method：表单提交方式 get/post-->
    - ```html
      <form action="save.php" method="POST"></form>
      ```

    * 基本控件

      - 单行文本框 type 属性设置为 text 的 input 元素可以创建单行文本框 单标签

      * ```html
        <!-- value:已经填好的值 -->
        <input type="text" value="132" />
        <!-- placeholder:提示文本，将以浅色文字写在文本框中，并不是文本框中的值 -->
        <input type="text" placeholder="请输入姓名" />
        <!-- disabled：用户不能与元素交互 即 锁死 -->
        <input type="text" disabled />
        ```

    - 单选按钮

      - 创建单选按钮

      * ```html
        <!-- 互斥的单选按钮可以设置他们的 name 为相同值
           单选按钮要有 value 值,向服务器提交的就是 value 值
           单选按钮如果加上了 checked 属性,表示默认被选中 -->
        <input type="radio" />
        ```

  * label 标签

    - ```html
      <!-- 标签用来将文字和单选按钮进行绑定，用户单击文字的时候也视为点击了单选按钮 -->
      <label> <input type="radio" name="sex" value="男" checked /> 男 </label>
      <label> <input type="radio" name="sex" value="女" /> 女 </label>
      <!-- 在 HTML4 时代，label 标签是通过 for 属性和单选按钮的 id 属性进行绑定的 -->
      <input type="radio" id="nan" /> <label for="nan">男</label>
      ```

  * 复选框
    - ```html
      <!--使用 type 属性值被设置为 checkbox 的< input>元素可以创建复选框  -->
      <input type="checkbox" />
      <!-- 同组复选框应该设置它们的 name 为相同值
            复选框要有 value 属性值,向服务器提交的就是 value 值 -->
      ```

  - 密码框

    - 使用 type 属性值被设置为 password 的< input>元素可以创建密码框
      - ```html
        <!--  <select>标签表示下拉菜单，value值是提交到服务器的 <option>是它内部的选项-->
        <select>
          <option value="alipay">支付宝</option>
          <option value="wx">微信</option>
          <option value="bank">网银</option>
        </select>
        ```

  - 多行文本框 < textarea>< /textarea>表示多行文本框

    - rows 和 cols 属性,用于定义多行文本框的行数和列数

    * ```html
      <p>
        留言：
        <textarea cols="100" rows="10"></textarea>
      </p>
      ```

  - 三种按钮
  - 表单中常见三种按钮,它们也都是 input 标签，type 属性值不同
    - type 属性值 按钮种类
      - button 普通按钮，可以简写为 `html <button> </button>`
      - submit 提交按钮
      - reset 重置按钮
  - input 类型总结
    - type 属性值 控件
      - text 单行文本框
      - radio 单选按钮
      - checkbox 多选按钮
      - password 密码框
      - button 普通按钮
      - reset 重置按钮
      - submit 提交按钮

  * html5 新增控件
    - 更丰富的 input 种类
    - type 属性值 控件
      ```html
      <p>
        颜色选择控件：
        <input type="color" />
      </p>
      ```
      - color 颜色选择控件
      - date、time 日期、时间选择控件
      - email 电子邮件输入控件
      - file 文件输入控件
      - number 数字输入控件
      - range 拖拽条
      - search 搜索框
      - url 网址输入控件
    - datalist 控件
      - <datalist>控件可以为输入框提供一些备选项，当用户输入的内容与备选项文字相同时,将会显示智能感应
      ```html
      <input type="text" list="province-list" />
      <datalist id="province-list">
        <option value="山西"></option>
        <option value="山东"></option>
        <option value="广西"></option>
        <option value="广东"></option>
        <option value="湖南"></option>
        <option value="湖北"></option>
        <option value="河南"></option>
        <option value="河北"></option>
      </datalist>
      ```

* 表格
  - table-tr-td 标签 表格-表格行-表格数据
  - table 表格标签
    - border 让表格显示边框 `html  <table border="1"> </table>`
    - caption 表格的标题 常常作为 table 的第一个子元素出现
      - ```html <table border="1" width="600">
        <caption>
          我是表格的标题
        </caption>
        <tr>
          <th>第一季度</th>
          <th>第二季度</th>
          <th>第三季度</th>
          <th>第四季度</th>
        </tr>
        ```
  * th 标题小格标签
  * 单元格的合并
    - colspan ：设置 td 或 th 的列跨度
    - rowspan ： 设置 td 或 th 的行跨度
  * thread tbody tfoot 标签
    - thread ：定义表头
    - tbody ： 定义表核心内容
    - tfoot ： 定义表脚，通常是汇总行
    - 被 css 替代的属性，也可以使用
      - cellpadding：定义表格单元的内容和边框之间的空间
      - cellspacing：百分比、像素定义两个表哥之间的大小

##### 转义字符

- &lt; ＜
- &gt; ＞
- &nbsp; 空格（不会被折叠）
- &copy; 版权符号 ©

##### 列表

- 注意事项
  - li 标签必须放到 ul 或 ol 中使用
  - ul 的子标签只能是 li
  - li 标签是容器，内部可以放其他任何标签
- 无序列表 ul-li
  - type 属性（disc：默认值 实心圆，cricle：空心圆，square：实心方块）定义前导符号的样式，被废弃，使用 css 替代
  ```html
  <ul>
    <li>面包</li>
    <li>牛奶</li>
    <li>鸡蛋</li>
    <li>水果</li>
  </ul>
  ```

```

* 有序列表 ol-li
  - type 属性 设置编号的类型（a：小写英文字母，A 大写英文字母，i：小写罗马数字，I：大写罗马数字，1：数字编码 默认）
  * start 属性 指定了列表编码的起始值 值应为阿拉伯数字
  * reversed 属性 指定列表中的条目是否是倒序排列的 只需要写单词，不需要值， html5 的新特性
* 定义列表 dl-dt-dd

##### sublime 快捷键

sublime 快捷键有：

Ctrl+D 选中光标所占的文本，继续操作则会选中下一个相同的文本。

Alt+F3 选中文本按下快捷键，即可一次性选择全部的相同文本进行同时编辑。

Ctrl+L 选中整行，继续操作则继续选择下一行。

Ctrl+Shift+L 在选中的每行行尾插入光标，即可同时编辑这些行。

Ctrl+Shift+M 选择括号内的内容。

Ctrl+M 光标移动至括号内结束或开始的位置。

Ctrl+Enter 在下一行插入新行。

Ctrl+Shift+Enter 在上一行插入新行。

Ctrl+Shift+[ 折叠选中代码。

Ctrl+Shift+] 展开选中代码。

Ctrl+K+0 展开所有折叠代码。

Ctrl+← 向左单位性地移动光标，快速移动光标。

Ctrl+→ 向右单位性地移动光标，快速移动光标。

shift+↑ 向上选中多行。

shift+↓ 向下选中多行。

Shift+← 向左选中文本。

Shift+→ 向右选中文本。

Ctrl+Shift+← 向左单位性地选中文本。

Ctrl+Shift+→ 向右单位性地选中文本。

Ctrl+Shift+↑ 将光标所在行和上一行代码互换。

Ctrl+Shift+↓ 将光标所在行和下一行代码互换。

Ctrl+Alt+↑ 向上添加多行光标，可同时编辑多行。

Ctrl+Alt+↓ 向下添加多行光标，可同时编辑多行。

Ctrl+J 合并选中的多行代码为一行。

Ctrl+Shift+D 复制光标所在整行，插入到下一行。

Tab 向右缩进。

Shift+Tab 向左缩进。

Ctrl+K+K 从光标处开始删除代码至行尾。

Ctrl+Shift+K 删除整行。

Ctrl+/ 注释单行。

Ctrl+Shift+/ 注释多行。

Ctrl+K+U 转换大写。

Ctrl+K+L 转换小写。

Ctrl+Z 撤销。

Ctrl+Y 恢复撤销。

Ctrl+F2 设置书签

Ctrl+T 左右字母互换。

F6 单词检测拼写。

Ctrl+F 打开底部搜索框，查找关键字。

Ctrl+shift+F 在文件夹内查找。

Ctrl+P 打开搜索框。

Ctrl+G 打开搜索框，自动带：，输入数字跳转到该行代码。

Ctrl+R 打开搜索框，自动带@，输入关键字，查找文件中的函数名。

Ctrl+： 打开搜索框，自动带#，输入关键字，查找文件中的变量名、属性名等。

Ctrl+Shift+P 打开命令框。

Esc 退出光标多行选择，退出搜索框，命令框等。

Ctrl+Tab 按文件浏览过的顺序，切换当前窗口的标签页。

Ctrl+PageDown 向左切换当前窗口的标签页。

Ctrl+PageUp 向右切换当前窗口的标签页。

Alt+Shift+1 窗口分屏。

Alt+Shift+2 左右分屏-2 列。

Alt+Shift+3 左右分屏-3 列。

Alt+Shift+4 左右分屏-4 列。

Alt+Shift+5 等分 4 屏。

Alt+Shift+8 垂直分屏-2 屏。

Alt+Shift+9 垂直分屏-3 屏。

Ctrl+K+B 开启/关闭侧边栏。

F11 全屏模式。

Shift+F11 免打扰模式。
```
