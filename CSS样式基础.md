# CSS3教程

vim：取消对ctrl + c的覆盖：
![image-20220703112621703](Typora_images/CSS样式基础/image-20220703112621703.png)



# CSS3基础教程：

视频教程：https://www.bilibili.com/video/BV1eW411T7Nr?from=search&seid=4282835502181908639&spm_id_from=333.337.0.0&vd_source=365d13057e58bb6a007cdd5275785229



CSS3规范文档：www.w3.org/TR/2011/REC-css3-selectors-20110929



项目路径：![image-20220618063241460](Typora_images/CSS样式基础/image-20220618063241460.png)

# 1、导学

**==<font color='blue'>css全称：cascading style sheets（层叠样式表）</font>==**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style type="text/css">
        /* 1、样式表
            2、样式表由规则组成 
            3、规则由选择器 和 {}的声明块组成
            4、声明块由css属性和css属性值组成的键值 构成
        */

        * {
            margin: 0px;
            padding: 0px;
        }
    </style>
</head>
<body>
    
</body>
</html>
```

- 基础的概念：样式表，规则，选择器，声明块，css属性，css属性值



```css
        /* 浏览器编译解析选择器的顺序 */
        div ul li #test {

        } 
```

**<font color='purple'>浏览器解析选择器的顺序，是从右往左的，因为这样子性能比较高；看上述的案例如果从左往右，他就得先遍历所有的div一个一个找过去，然后再遍历所有的ul一个一个找过去，那太sb了。。。。。所以从右往左进行解析，解析遇到#test直接找到了，然后就不需要去解析li了对吧，性能上会搞很多的</font>**



# 2、选择器

以后所有的前端都在MDN上进行查找就行了。

https://developer.mozilla.org/zh-CN/docs/Learn



## 2.1、基础选择器

基础选择器类型 6种

```c
        /* 
        通配符选择器  

        id #
        类 .
        元素选择器 div
        后代选择器 空格
        分组选择器  , (结合符)
        */

```

案例：
![image-20220618070732160](Typora_images/CSS样式基础/image-20220618070732160.png)





**<font color='purple'>选择器的声明具有优先级顺序，而不是选择器</font>**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style type="text/css">

        /* 
        通配符选择器  

        id #
        类 .
        元素选择器 div
        后代选择器 空格
        分组选择器  , (结合符)
        */

        /*
        平常我们所说的选择器的优先级其实是一个错误的概念，
        准确的来说应该是声明的优先级
        */
        h1,h2,h3 {
            color: pink; 
        }

        #test {
            color: deeppink
        }
    </style>
</head>
<body>
    <div id="wrap">
        <h1 id="test">1-1 </h1>
        <h2>2-2</h2>
        <h3>3-3</h3>
    </div>
    
</body>
</html>
```



## 2.2、子元素选择器

- **<font color='red'>就是 > 符号，和后代选择器不同的是，这个东西只会选择它的儿子</font>**

```css
    <style type="text/css">
        /*
            > 这个东西只会选择儿子
        */
        .wrapper > div{
            color: pink;
        }

    </style>
```

```html
<body>
    <div class="wrapper">
        <div>
            1-1
            <div>1-1-1</div>
        </div>
        <div>1-2</div>
        <div>1-3</div>
        <div>1-4</div>
    </div>
</body>
```

**结果：**
![image-20220618072041446](Typora_images/CSS样式基础/image-20220618072041446.png)

- ***<font color='blue'>为什么 1-1-1也变成pink了呢？他又没有被选择到？？？？</font>***

- **<font color='red'>因为它继承了div.wrapper的样式，所以在css中还要注意：css默认值和继承值</font>**

![image-20220618072325801](Typora_images/CSS样式基础/image-20220618072325801.png)



## 2.3、相邻弟弟选择器

- 符号就是 + 

```html
    <style type="text/css">
        #wrapper > .first + .inner {
            color: pink;
        }
    </style>
</head>
<body>
    <div id="wrapper">
        <div class="inner">inner</div>
        <div class="first">first</div>
        <div class="inner">inner</div>
        <div class="inner">inner</div>
        <div class="inner">inner</div>
    </div>
</body>
```

结果：
![image-20220618073335308](Typora_images/CSS样式基础/image-20220618073335308.png)

**==<font color='red'>只有紧挨着first元素的下一个元素才可以被选择</font>==**

- 如果改成这样：

```html
    <div id="wrapper">
        <div class="inner">inner</div>
        <div class="first">first</div>
        <div></div>
        <div class="inner">inner</div>
        <div class="inner">inner</div>
        <div class="inner">inner</div>
    </div>
```

结果：
![image-20220618073606819](Typora_images/CSS样式基础/image-20220618073606819.png)

## 2.4、通用弟弟选择器

- 就是 ~ 这个符号

```html
    <style type="text/css">
        #wrapper .first ~ .inner{
            border: 1px solid red;
        }
    </style>
</head>
<body>
    <div id="wrapper">
        <div class="inner">inner</div>
        <div class="first">first</div>
        <div class="nihao">你好呀，设备</div>
        <div class="inner">inner</div>
        <div class="inner">inner</div>
        <div class="inner">inner</div>
        <div class="inner">inner</div>
    </div>
</body>
```

结果：
![image-20220618074915602](Typora_images/CSS样式基础/image-20220618074915602.png)

***==<font color='blue'>~通用兄弟选择器和+相邻兄弟选择器不同在于 他不用紧挨，只要是下面的都是兄弟（同一个父框框）;还有他不会匹配兄弟的儿子</font>==***

```html
    <div id="wrapper">
        <div class="inner">inner</div>
        <div class="first">first</div>
        <div class="nihao">你好呀，设备</div>
        <div class="inner">inner<div class="inner">zzw</div></div>
        <div class="inner">inner</div>
        <div class="inner">inner</div>
        <div class="inner">inner</div>
    </div>
```

![image-20220618075311855](Typora_images/CSS样式基础/image-20220618075311855.png)

**==<font color='red'>在这里之所以我们要选择border属性就是因为它不会被继承的、可以更加的直观。</font>==**



## 2.5 、属性选择器



```html
    <div id="wrapper">
        <div name="" style="" fkadsljf=""></div>
    </div>
```

- **<font color='red'>在html标签中我们可以自定义属性的，一般我们把这些属性都称之为attrs ，然后style是一个标签的属性和css没有任何关系，但是它的值和css样式有关系，这个逻辑要理清楚。</font>**

### 2.5.1、属性存在选择器

- **目标选择器[属性名]**

```html
    <style type="text/css">
        * {
            margin: 0px;
            padding: 0px;
        }

        div[name] {
            border: 1px solid blue;
        }
    </style>
</head>
<body>
    <div id="wrapper">
        <div name="zzw  ">zzw</div>
        <div name="xujei">xujie</div>
        <div name="xujieru ">xujieru</div>
        <div name="shaoyingfei ">shaoyingfei</div>
    </div>
</body>
```

**==<font color='red'>就是选择含有name属性的div</font>==**

### 2.5.2、属性值选择器

就两个

- div[name="zzw"]
- div[name~="zzw"]

```html
    <style type="text/css">
        * {
            margin: 0px;
            padding: 0px;
        }

        div[name="xujie"] {
            border: 1px solid blue;
        }
    </style>
</head>
<body>
    <div id="wrapper">
        <div name="zzw">zzw</div>
        <div name="xujie">xujie</div>
        <div name="xujieru ">xujieru</div>
        <div name="shaoyingfei ">shaoyingfei</div>
    </div>
</body>
```

***==<font color='blue'>关注一下细节，你看就是属性选择器[]中的表达式和 div标签中的表达式其实是完全一样的对吧</font>==***



***<font color='red'>第二个就是 约等于的意思</font>***

![image-20220618092023418](Typora_images/CSS样式基础/image-20220618092023418.png)

```html
    <style type="text/css">
        * {
            margin: 0px;
            padding: 0px;
        }

        /**约等于许洁 **/
        div[name~="xujie"] {
            border: 1px solid blue;
        }
    </style>
</head>
<body>
    <div id="wrapper">
        <div name="zzw">zzw</div>
        <div name="xujie zzw">xujie</div>
        <div name="xujieru ">xujieru</div>
        <div name="shaoyingfei ">shaoyingfei</div>
    </div>
</body>
```



### 2.5.3、CSS3属性值选择器

![image-20220618092553197](Typora_images/CSS样式基础/image-20220618092553197.png)

- [attr|=val]

```html
        div[name|="zzw"] {
            border: 1px solid red;
        }

    </style>
</head>
<body>
    <div id="wrapper">
        <div name="zzw">zzw</div>
        <div name="zzw-ss">zzw-ss</div>
        <div name="zzw_ss">zzw-ss</div>
        <div name="zzwss">zzw-ss</div>
```



![image-20220618092854475](Typora_images/CSS样式基础/image-20220618092854475.png)



**==显然它只能选择 zzw和zzw-ss==**



- [attr^=val]

**这个^叫做拖字符，正则里也有代表匹配开始的位置**

```html

//样式
div[name^="xujieru"] {
            border: 1px solid yellowgreen;
        }

//代码
<div name="xujieru">xujieru</div>
        <div name="xujieru-fd">xujieru-fd</div>
        <div name="xujieru_fd">xujieru_fd</div>
        <div name="xujierufd">xujierufd</div>
        <div name="xujieru fjkj">xujieru fjkj</div>
```

这个结果没有什么疑问都是能匹配到的，因为它相当于正则
![image-20220618093543696](Typora_images/CSS样式基础/image-20220618093543696.png)

- [attr$=val]和[attr*=val]就没有什么用了。



## 2.6、伪类与伪元素选择器

**<font color='red'>伪类和伪元素是不存在与dom树当中的。之所以要设计伪类和伪元素的选择器，就是让CSS有能力选中这些不在dom树中的东西</font>**

- ***伪类是用来拿到dom节点的状态***

- ***伪元素是真的元素，只不过它不在dom树中的。***

### 2.6.1、链接伪类

![image-20220618095013150](Typora_images/CSS样式基础/image-20220618095013150.png)

**==<font color='red'>因为a标签的的 :link 和 :visited 已经覆盖了所有的a标签的所有状态（点过和没点过）所以如果在a标签中要加入 :hover 和 :active属性，就必须放在link和visited的后面才行，也就是 l v h a</font>==**

==注意：在visited中只有color、backgroud-color、border-color能被访问到！其他属性都没有用，这是定死的！！！==

#### 2.6.1.1、纯CSS做选项卡

- 专属于a标签的 target的灵活运用

```html
    <style type="text/css">
        a {
            text-decoration: none;
            color: pink;
        }

        div {
            width: 100px;
            height: 100px;
            background-color: pink;
            text-align: center;
            font: 32px/100px "微软雅黑";
            display: none;
        }
        :target {
            display: block;
        }
    </style>
</head>
<body>
    <a href="#div1">商品列表</a>
    <a href="#div2">购物车列表</a>
    <a href="#div3">我的</a>
    <div id="div1">
        c++
    </div>
    <div id="div2">
        fjsldkj
    </div>
    <div id="div3">
        zzw
    </div>

</body>
```

效果：
![image-20220618104431764](Typora_images/CSS样式基础/image-20220618104431764.png)



**<font color='red'>这里可以总结出三个知识点：</font>**

- **target作用于在浏览器地址栏的url中出现过的片段的标签，(就是当#div3在url中出现的时候，css的target就会找到id是div3的属性，然后把自己的 声明块中的属性添加到div3上去就行了)**

- **a标签不换行的.**

- **框框内字体居中**

   **text-align: center;**

  **font: 字体大小/框框高度   字样**



### 2.6.2、动态伪类

:hover和:active

```html
    <style type="text/css">
        * {
            margin: 0px;
            padding: 0px;
        }
        .inner {
            font-size:32px;
            color: black;
        }
        .inner:hover {
            font-size:48px;
            color: purple;
        }
        .inner:active {
            font-size:78px;
            color: pink;
        }

    </style>
</head>
<body>
    <div id="wrapper">
        <div class="inner">zzejflkejlkjlkjlkjfei j</div>
    </div>
```

==hover不用多说，active就是当keydown的时候触发的==

### 2.6.3、表单伪类



![image-20220622071251376](Typora_images/CSS样式基础/image-20220622071251376.png)

```html
    <style type="text/css">
        * {
            margin: 0px;
            padding: 0px;
        }
        input:enabled {
            background: yellow;
        }
        input:disabled {
            background: deepskyblue;

        }
        /** 这个样式只对复选框有作用*/
        input:checked {
            width: 100px;
            height: 100px;
        }

        input:focus {
            /* border: 2px solid red; */
            background: pink;
        }

    </style>

</head>
<body>
    <input type="text" placeholder="请输入一些内容">
    <input type="text" placeholder="请输入一些内容" disabled>
    <input type="checkbox">
    <input type="text" placeholder="请输入一些内容">
</body>
```

**==<font color='red'>:checked伪类只对复选框有作用，如果input是disabled，那么:focus状态不会生效的。</font>==**



https://www.jianshu.com/p/170d1332e29b：行内元素，块级元素，行内-块级元素说明。



### 2.6.4、自定义单选框

- 最基础的单选框

```html
    <label>
        <input type="radio" name="radioGroup">
        <span>zzw</span>
    </label>
    <label>
        <input type="radio" name="radioGroup">
        <span>xujie</span>
    </label>
    <label>
        <input type="radio" name="radioGroup">
        <span>lty</span>
    </label>
```

![image-20220622074735400](Typora_images/CSS样式基础/image-20220622074735400.png)

**==<font color='red'>这里的单选框有两个要点，第一：只有name相同，单选框才会生效；第二：label标签可以将radio和span关联起来，然后点击span就能够使得单选框选中，这是实现自定义单选框的基础铺垫。</font>==**



具体实现：

```html
    <style>        
label {
            /** 因为label是一个内联元素，所以只用width和height是没有效果的，
                使用float可以将内联元素转换成块级元素，这样，width和height就有效了
                当然使用absolute也可以使得label的宽和高生效的。
            */
            float: left;
            position: relative;
            width: 50px;
            height: 50px;
            border: 1px solid blue;
        }

        input {
            position: absolute;
            top: -100px  /** 隐藏元素*/
        }

        span {
            position: absolute;
            width: 50px;
            height: 50px;
            /** 当然你也可以不用设置w和h直接设置top:0 left:0 ...就行了*/
        }


        label > input:checked + span {
            background: pink;
        }

    </style>

</head>
<body>
    <label>
        <input type="radio" name="radioGroup">
        <span></span>
    </label>
    <label>
        <input type="radio" name="radioGroup">
        <span></span>
    </label>
    <label>
        <input type="radio" name="radioGroup">
        <span></span>
    </label>

    
</body>
```

**==<font color='red'>label和span都是内联元素，所以要设置宽和高时，需要设置position:absolute;或者float:left;然后就是兄弟选择器的妙用了，哈哈太秀了</font>==**

![image-20220622081648381](Typora_images/CSS样式基础/image-20220622081648381.png)



## 2.7、结构性伪类

***==<font color='red'>nth-child(index)系列和nth-of-type(index)系列，注意index最小从1开始!!!</font>==***

示例：这段代码会生效么？

```html
    <style type="text/css">
        * {
            margin: 0px;
            padding: 0px;
        }

        .wrap ul > li:nth-child(1) {
            color: pink;
        }

    </style>
</head>
<body>
    <div class="wrap">
        <ul>
            <p></p>
            <li>1</li>
            <li>2</li>
            <li>3</li>
        </ul>
    </div>

    
</body>
```

输出：
![image-20220622083231864](Typora_images/CSS样式基础/image-20220622083231864.png)

**==<font color='red'>为什么不生效了呢？因为.wrap ul > li:nth-child(1)的真正含义是：找到.wrap下面的所有ul，然后找到ul下面的第一个子元素，并且这个子元素一定要是li，不然就不生效了。</font>==**



- 再看看nth-of-type

```html
        .wrap ul > li:nth-child(1) {
            color: pink;
        }

        .wrap ul > li:nth-of-type(1) {
            color: red;
        }

    </style>
</head>
<body>
    <div class="wrap">
        <ul>
            <p></p>
            <li>1</li>
            <li>2</li>
            <li>3</li>
        </ul>
    </div>
```

输出：
![image-20220622084311120](Typora_images/CSS样式基础/image-20220622084311120.png)

**==<font color='red'>它是找到ul下面第一次出现的li和nth-child的找到第一个子元素不太一样的</font>==**

### 2.7.1、nth-child衍生

![image-20220624161318369](Typora_images/CSS样式基础/image-20220624161318369.png)



#### part1:first-child（没有索引）

- ***first-child***

```html
        :first-child {
            border: 1px solid red;
        }


    </style>
</head>
<body>
    <div class="wrap">
        <ul>
            <p></p>
            <li>1</li>
            <li>2</li>
            <li>3</li>
        </ul>
    </div>
```

输出：


![image-20220624161739860](Typora_images/CSS样式基础/image-20220624161739860.png)

**==如果不指定选择器的话，那么每一个大儿子都会有border的，相当于前面加了一个*==**

```css
        p:first-child {
            border: 1px solid red;
        }
```

==这个表示是 是第一个儿子并且是p标签的元素。==

#### part2:last-child（没有索引）

和first-child是一样的，只不过是最后一个儿子，并且是p标签



#### part3:nth-last-child（有索引）

这个是nth-child的倒序版本而已



#### part4:only-child（没有索引）

这个相当于是 :first-child和:last-child的组合选择器。说明只能有一个子元素！！！

```html
        li:only-child {
            border: 1px solid pink;
        }

    </style>
</head>
<body>
    <div class="wrap">
        <ul>
            <li>2</li>
        </ul>
    </div>
```

输出：
![image-20220624163141334](Typora_images/CSS样式基础/image-20220624163141334.png)







### 2.7.2、nth-of-type衍生

其余的都和nth-child的衍生是差不多的，不过最后一个only-of-type有一点不一样

```html
        p:only-of-type{
            border: 1px solid purple;
        }


    </style>
</head>
<body>
    <div class="wrap">
        <ul>
            <li>2</li>
            <li>2</li>
            <li>2</li>
            <li>2</li>
            <p>3</p>
            <li>2</li>
            <li>2</li>
        </ul>
    </div>
```

==nth-of-type的真正含义应该是仅仅出现一次！==



### 2.7.3、结构性伪类的坑

```html
        #wrapper .inner:nth-of-type(1) {
            border: 1px solid red;
        }
    </style>
</head>
<body>
    <div id="wrapper">
        <div class="inner">div</div>
        <p class="inner">p</p>
        <h1 class="inner">h1</h1>
        <h2 class="inner">h2</h2>
    </div>
```

看看结果：

![image-20220702124556831](Typora_images/CSS样式基础/image-20220702124556831.png)

**<font color='red'>为什么明明nth-of-type(1)，却选中了所有的元素呢？这就是nth-of-type坑的地方了，就是说它在编译的时候会把.inner编译成含有.inner类的元素名，所以就相当于</font>**

```css
        #wrapper div:nth-of-type(1) {
            border: 1px solid red;
        }

        #wrapper p:nth-of-type(1) {
            border: 1px solid red;
        }
......
```

**<font color='red'>这就是它的大坑！</font>**



### 2.7.4、面试题

- **最后一项没有 横杠**

![image-20220702130211011](Typora_images/CSS样式基础/image-20220702130211011.png)



```html
        div > a:not(:last-child) {
            border-right: 2px solid red;
        }

    </style>
</head>
<body>
    <div>
        <a href="#">选项卡一</a>
        <a href="#">选项卡二</a>
        <a href="#">选项卡三</a>
        <a href="#">选项卡四</a>
        <a href="#">选项卡五</a>
        <a href="#">选项卡六</a>
    </div>
```

**==<font color='red'>重点就是:not(:last-child)这个东西</font>==**



- 给空元素指定特殊样式：**:empty伪类**

```html
        div > a:empty {
            background: blue;
        }
    </style>
</head>
<body>
    <div>
        <a href=""></a>
```



## 2.8、伪元素选择器

**==<font color='deeppink'>伪元素选择器就一个before和after，用他们的时候要注意一定要加content:""就行，还可以使用display:block;这样的改变他们的块级状态</font>==**

- ::first-letter 第一个字母
- ::first-line  第一行
- ::selected  被选中时候的状态

这些都很简单



## 2.9、根元素选择器

**<font color='deeppink'>:root 这就用来选中html标签的，要知道</font>**





# 3、声明的优先级

## 3.1、选择器特殊性

![image-20220702134801654](Typora_images/CSS样式基础/image-20220702134801654-16567408854501.png)

**==<font color='deeppink'>只要明白一点，就是如果有规则有冲突，那么特殊性越大的优先级越高！如果特殊性一样，那么声明在后面的会覆盖声明在前面的</font>==**

## 3.2、重要声明

![image-20220702135535330](Typora_images/CSS样式基础/image-20220702135535330.png)

重要声明优先级考虑：

![image-20220702135850608](Typora_images/CSS样式基础/image-20220702135850608.png)



# 4、自定义字体&字体图标

字体图标：

![image-20220703110447224](Typora_images/CSS样式基础/image-20220703110447224.png)

- 这个东西就是字体图标

- 字体图标的好处：

  - 矢量图不会失真
  - 大小通过font-size调整（哈哈，难怪那个anti-design-vue的图标大小也是用font-size调整的，哈哈）

  - 而且不用从后台获取，减少带宽消耗，提升系统性能



## 4.1、自定义字体

操作系统中所有的自带字体如下所示：C:\Windows\Fonts
![image-20220703111145801](Typora_images/CSS样式基础/image-20220703111145801.png)







==操作系统的自带字体，浏览器不一定能用的，因为还要看浏览器对字体的支持情况。==





```html
        .test {
            font: bold 50px "Lucida Sans";
        }

    </style>
</head>
<body>
    <div class="test">
        圆滚滚，QHF
    </div>
```

==这里的font是一个联合属性：分别是font-weight、font-size和font-family的联合==



### 4.1.1、UI自定义字体

在本地目录下，放一个字体文件，然后就可以引用它了
![image-20220703113749148](Typora_images/CSS样式基础/image-20220703113749148.png)



```html
        @font-face {
            font-family: "my-font-zzw";
            src: url(./font/ALGER.TTF);
        }

        .test {
            font: bold 50px "my-font-zzw";
        }

    </style>
</head>
<body>
    <div class="test">
        HTJK，Just Do It!
    </div>
```

效果：
![image-20220703113817604](Typora_images/CSS样式基础/image-20220703113817604.png)



==一般情况下，这个字体文件都放在服务器上，然后使用@font-face的src指向字体的url就行了==



### 4.1.2、字体图标

***到底什么是自定义字体？***

#### **==<font color='deeppink'>所谓自定义字体，其实就是把汉字、英文字母 和一张矢量图对应起来，这张矢量图上面就是各种好看的字体样式了！根据这个原理，所以我们可以把一些字符和矢量图标联系在一起，从而生成字体图标了！</font>==**

#### part1、生成字体图标的方法

网站：https://icomoon.io/app/#/select

![image-20220703143734913](Typora_images/CSS样式基础/image-20220703143734913.png)



![image-20220703143830648](Typora_images/CSS样式基础/image-20220703143830648.png)



**==<font color='red'>可以download到一个压缩包，这个压缩包里面就是示例，可以根据这个示例来使用你的字体图标就行了。</font>==**



***使用说明：***

原理：

![image-20220703144538645](Typora_images/CSS样式基础/image-20220703144538645.png)



使用：
![image-20220703145817642](Typora_images/CSS样式基础/image-20220703145817642.png)



# 5、C3新增UI样式

## 5.1、新增文本样式

- 文本新增样式
  - opacity（老的是用：visibility）**==<font color='red'>注意：opacity不是一个可以继承的属性，但是可以影响到自己的子元素！</font>==**
  - rgba （可以定义透明度了）![image-20220704214602758](Typora_images/CSS样式基础/image-20220704214602758.png)

**==<font color='deeppink'>以后rgba的标准写法都用.x的形式，前面不要再加0了！</font>==**



### 5.1.1、小需求

文字透明,背景不透明；背景透明，文字不透明

**==<font color='deeppink'>很简单只要是用rgba修改color和background就行了</font>==**

- tips:超级好用的捏！

![image-20220704215414200](Typora_images/CSS样式基础/image-20220704215414200.png)

### 5.1.2、文字阴影（text-shadow属性）

```html
        .test {
            text-align: center;
            /** 第二个是指定它的行高！line-height:可以是一个px值（如果要居中的话，就设定它是盒子的高就行了），也可以是1.5小数*/
            font: 100px/200px "微软雅黑";
            /** 阴影颜色，阴影x轴偏移值，阴影y轴偏移值，阴影模糊像素，越高越模糊
                你可以叠加多层模糊的
            */
            text-shadow: purple 10px 10px 20px,pink 15px 15px 25px;
        }

    </style>
</head>
<body>

    <div class="test">
        尚硅谷
    </div>
```

**==<font color='purple'>text-shadow有4个属性，分别是阴影颜色、x方向偏移量、y方向偏移量、模糊度；可以叠加多个阴影</font>==**

![image-20220704221447183](Typora_images/CSS样式基础/image-20220704221447183.png)

#### part1：浮雕字体

```html
        body {
            background-color: blueviolet;
        }

        .test {
            text-align: center;
            font: 100px/200px "微软雅黑";
            color: blueviolet;
            text-shadow: black 2px 2px 8px;
        }
    </style>
</head>
<body>
    <div class="test">
        行天道，无后悔！
    </div>
```

效果：


![image-20220704223516486](Typora_images/CSS样式基础/image-20220704223516486.png)



### 5.1.3、背景图片透明模糊

**==<font color='purple'>这个需求是一个经典需求啊！</font>==**

```html
        .wrapper {
            position: relative;
            background: rgba(0,0,0,.5);
        }

		img {
            /** 上右下左*/
            margin: 50px 0 50px 50px;
        }

        .wrapper .bg {
            position: absolute;
            top: 0;
            bottom: 0;
            left: 0;
            right: 0;
            background: url(img/bg.jpg) no-repeat ;
            z-index: -1;
            /** 这个东西是模糊整个元素的 */
            filter: blur(3px);
        }
    </style>
</head>
<body>
    <div class="wrapper">
        <!-- 这里使用img标签把wrapper容器撑开了,因为img标签是block元素 -->
        <img src="img/people.jpg" alt="" width="200">
        <div class="bg">
        </div>
    </div>
```

要点：

- 背景颜色透明、绝对定位、top控制大小、z-index
- **==<font color='deeppink'>最重要的：就是filter: blur();这个函数，在C3中，这个函数是用来模糊的，而且会模糊一整个元素的！</font>==**

![image-20220704230556399](Typora_images/CSS样式基础/image-20220704230556399.png)

### 5.1.4、文字描边

![image-20220704230722831](Typora_images/CSS样式基础/image-20220704230722831.png)

- ***他需要webkit的内核支持才行！***

- 不太会用到

### 5.1.5、文字排版

```html
        /** C3文字排版*/
        div {
            width: 200px;
            height: 200px;
            border: 1px solid red;
            /** 文字排版方向*/
            direction: rtl;
            unicode-bidi: bidi-override;
        }

    </style>
</head>
<body>
    <div>
        尚硅谷
    </div>
```

==- direction控制文字方向，unicode-bidi:控制文字内的方向==



#### part1: 文字过多时候省略！

```html
    <div>
        尚硅谷尚硅谷尚硅谷尚硅谷尚硅谷尚硅谷尚硅谷尚硅谷尚硅谷尚硅谷尚硅谷尚硅谷尚硅谷尚硅谷尚硅谷尚硅谷尚硅谷尚硅谷尚硅谷尚硅谷尚硅谷
    </div>
```

如果你这样写的话，会发现它换行了
![image-20220704232221914](Typora_images/CSS样式基础/image-20220704232221914.png)

==不让他换行的办法：==

```css
        div {
            width: 200px;
            height: 200px;
            border: 1px solid red;
            /** 文字排版方向*/
            /* direction: rtl; */
            /* unicode-bidi: bidi-override; */
            /** 禁止文字换行*/
            white-space: nowrap;
        }
```

==显示省略号的方法：==

```css
            overflow: hidden;
            text-overflow: ellipsis;
```



**==<font color='deeppink'>注意：如果display为inline的话，就不能显示省略号了，因为元素是由内容撑开的了！</font>==**







## 5.2、盒模型新增样式

**前端中的x轴和y轴的方向如下：**
![image-20220706061230442](Typora_images/CSS样式基础/image-20220706061230442.png)

==这个很重要，不能忘记的！==





### 5.2.1、盒子阴影

#### part1：水平垂直居中的方案

```css
        .test {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: violet;
            width: 300px;
            height: 300px;
            /** 这个属性必须要加上的！不然就不行*/
            margin: auto;
        }
```

**==<font color='red'>注意：</font>==**

- ***==<font color='deeppink'>width和height是必须要定下来的，不然就会变成这样张开来</font>==***

![image-20220706062328026](Typora_images/CSS样式基础/image-20220706062328026.png)

- ***==<font color='deeppink'>这里的margin: auto也是必须的，不然会变成这样的</font>==***

![image-20220706062426001](Typora_images/CSS样式基础/image-20220706062426001.png)

- ***==<font color='deeppink'>top、left的百分比是相较于父盒子的宽度和高度来定的</font>==***

![image-20220706064702015](Typora_images/CSS样式基础/image-20220706064702015.png)



#### part2：box-shadow

**继承性：不可以继承！**

```css
        .test {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: violet;
            width: 300px;
            height: 300px;
            /** 这个属性必须要加上的！不然就不行*/
            margin: auto;

            box-shadow: 13px 13px 13px black;
        }
```

![image-20220706065225335](Typora_images/CSS样式基础/image-20220706065225335.png)

==box-shadow: 参数->x轴偏移量，y轴偏移量， 模糊程度， 颜色（和text-shadow一样可以叠加多个阴影的）；相较于text-shadow，还有两个参数==

```css
            box-shadow: 13px 13px 13px 20px black inset;
```

**==<font color='deeppink'>参数四表示阴影的大小；最后一个表示阴影的往内还是往外的</font>==**

### 5.2.2、倒影

这个和文字描边一样都是需要webkit内核才行的。



![image-20220706070728153](Typora_images/CSS样式基础/image-20220706070728153.png)



#### part1：图片水平垂直居中的方案

方案一：

```css
        /** 图片水平垂直居中的方案一*/
        /* img {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0; 
            margin: auto;
        } */
```

**==<font color='violet'>这个方案有一个坏处，就是把img元素变成浮动的了（难怪需要子绝父相）</font>==**

```css
        /** 方案二*/
        /** 首先要撑开body，这里之所以要加一个html，是因为body在html里面，所以
        要先设置html，才能把body也设置为屏幕高度的100%*/
        html,body {
            height: 100%;
        }

        body {
            text-align: center;
        }

        body::after {
            content: "";
            height: 100%;
            display: inline-block;
            /** 竖直对齐方式*/
            vertical-align: middle;  
        }

        img {
            vertical-align: middle;  
        }
```

**==<font color='deeppink'>这个居中的原理就很骚了，因为::after和img在渲染的时候是兄弟元素，对吧，所以把::after高度设置为100%（宽度为0），然后设置inline-block，把::after和img的竖直对齐都设置为middle，img就会参照::after的middle了所以是竖直居中。</font>==**

- img也是inline-block，和::after是同一个级别的
- 级别相同，谁高听谁的

#### part2：倒影

```html
        html,body {
            height: 100%;
        }

        body {
            text-align: center;
        }

        body::after {
            content: "";
            height: 100%;
            display: inline-block;
            /** 竖直对齐方式*/
            vertical-align: middle;  
        }

        img {
            vertical-align: middle;  
			/** 倒影方向，以及与原图的距离*/
            -webkit-box-reflect: right 10px;
        }

    </style>
</head>
<body>
    <img src="./people.jpg" alt="" width="245px">
</body>
```

![image-20220706074157582](Typora_images/CSS样式基础/image-20220706074157582.png)

### 5.2.3、任意调整元素大小（resize）

![image-20220706074750727](Typora_images/CSS样式基础/image-20220706074750727.png)

```html
        .test {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: violet;
            width: 300px;
            height: 300px;
            /** 这个属性必须要加上的！不然就不行*/
            margin: auto;

            resize: both;
            overflow: auto;

        }
    </style>
</head>
<body>
    <div class="test">

    </div>
```

### 5.2.4、box-sizing

#### part1：第三种居中方案

```css
        .test {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 300px;
            height: 300px;
            margin-left: -150px;
            margin-top: -150px;
            background-color: violet;
        }
```



这种方案本来是很好的，但是如果加了padding呢？

```css
        .test {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 300px;
            height: 300px;
            margin-left: -150px;
            margin-top: -150px;
            background-color: violet;

            padding: 50px;

        }
    </style>
</head>
<body>
    <div class="test">
    </div>
```

![image-20220706080602099](Typora_images/CSS样式基础/image-20220706080602099.png)

**==<font color='violet'>他不居中的原因是因为，padding的值也被算在盒子的宽和高里面了。。。想要避免这种情况的发生，只能使用box-sizing: border-box</font>==**

```css
        .test {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 300px;
            height: 300px;
            margin-left: -150px;
            margin-top: -150px;
            background-color: violet;

            padding: 50px;
            box-sizing: border-box;

        }
```





#### part1：输入框的右边偏移

box-size: border-box在输入框中也很常用的，嘻嘻

```css
        input[type="text"] {
            width: 245px;
            padding-left: 50px;
            box-sizing: border-box;
            background-color: aqua;
        }
```

![image-20220706081747403](Typora_images/CSS样式基础/image-20220706081747403.png)



==难怪要在* {}添加border-box了，哈哈懂了==



## 5.3、圆角新增的样式

```css
        .test {
            width: 200px;
            height: 200px;
            position: absolute;
            top: 50%;
            left: 50%;
            margin-left: -100px;
            margin-top: -100px;
            border: 3px solid purple;
            border-radius: 50%;
        }
```

![image-20220706230047529](Typora_images/CSS样式基础/image-20220706230047529.png)

**==<font color='red'>这里为什么是一个圆捏？因为border-radius的值就是一个圆形的半径，50%说明半径是100px，然后生成一个圆把原来的框框隐藏掉了（而又因为一个框框中，生成的圆的最大半径必然是50%所以就算你写70%也不会有任何的变化的。。。）</font>==**



```css
            border-radius: 10px;
```

![image-20220706230435180](Typora_images/CSS样式基础/image-20220706230435180.png)



**==<font color='purple'>要想了解这个属性，就必须要知道它产生圆角的原理，其实很简单，就是产生上、右、下、左的半径为10px的圆，然后去和左上、右下...这些方向上的直角进行香蕉、裁剪操作，然后就可以得到圆角了。知道了原理就知道了另一种很骚的写法了，哈哈</font>==**

```css
            border-radius: 10px 20px 30px 45px;
```

![image-20220706230844643](Typora_images/CSS样式基础/image-20220706230844643.png)



两个值的写法：

```css
           border-radius: 10px 50px;
```

![image-20220706231620985](Typora_images/CSS样式基础/image-20220706231620985.png)

==/斜杠是后面的值，\\是前面的值==



### 5.3.1、长半轴和短半轴

说白了就是水平半轴和竖直半轴，这两个方向上的长度，长度一样的时候就是圆，长度不一样的时候就是椭圆了，嘻嘻

```css
            border-radius: 20px/60px ;
```

![image-20220707060620799](Typora_images/CSS样式基础/image-20220707060620799.png)



- 两个值的写法：

```css
            border-radius: 20px/60px 20px;
```

![image-20220707061121317](Typora_images/CSS样式基础/image-20220707061121317.png)

**==<font color='purple'>\\方向上是一个短半轴20px，长半轴40px的椭圆；/方向上是一个短半轴为20px（由开头第一个值定的）长半轴也为20px的圆。</font>==**



- 画一个正常的椭圆（从矩形里面画）

```css
        .test {
            width: 200px;
            height: 300px;
            position: absolute;
            top: 50%;
            left: 50%;
            margin-left: -100px;
            margin-top: -100px;
            border: 3px solid purple;
            /* border-radius: 10px 20px 30px 45px; */
            border-radius: 100px/150px;
        }
```



![image-20220707061649743](Typora_images/CSS样式基础/image-20220707061649743.png)

### 5.3.2、注意

**==<font color='purple'>在手机端开发的时候尽量不要用%，而是用px来确定长半轴和短半轴的值</font>==**







# CSS3flex布局

教程：https://www.bilibili.com/video/BV1N54y1i7dG?from=search&seid=17813754073632202728&spm_id_from=333.337.0.0&vd_source=365d13057e58bb6a007cdd5275785229



![image-20220618114118491](Typora_images/CSS样式基础/image-20220618114118491.png)



- **<font color='red'>使用flex布局之后就没有什么行内元素和块级元素的区分了，都是有大小的！</font>**



# 1、flex布局原理

- **==<font color='purple'>flex布局全称是flexible Box布局，就是弹性布局的意思，任何一个容器都可以指定为flex布局的！！！不论它是行内元素还是块级元素</font>==**

- **==<font color='red'>当我们为父盒子设定flex布局的时候，子元素的float、clear和vertical-aligin属性都将失效</font>==**

- **==<font color='blue'>设置了flex布局的盒子被称为 flex container，弹性盒子；里面的每一个项目被称为 flex item项</font>==**

- ***==通过设置父盒子的flex相关属性和子盒子的flex相关属性就可以完成flex的布局了==***



# 2、Container属性相关

**==<font color='red'>主要有六种属性：</font>==**

![image-20220618120810771](Typora_images/CSS样式基础/image-20220618120810771.png)

**六个里面主要是 align-content和flex-flow还不太熟悉**



## 2.1、flex-direction属性值

![image-20220618175538899](Typora_images/CSS样式基础/image-20220618175538899.png)

- **<font color='red'>这里最重要的还是row和column，另外两个真的没有必要。</font>**

## 2.2、justify-content属性

![image-20220621212159251](Typora_images/CSS样式基础/image-20220621212159251.png)

- **<font color='red'>注意space-around和space-between两者的区别，一个是直接平分剩余空间，一个是先贴边再平分。</font>**



## 2.3、flex-wrap属性

**<font color='purple'>flex布局有比较特殊的情况，就是当一行内盒子的总体宽度超过容器框框的宽度，那么，盒子们的宽度会被压缩的。</font>**

```css
        .container { 
            display: flex;
            width: 800px;
            height: 500px;
            background-color: pink;
            /** 默认主轴是x轴，也就是行*/
            /** 元素是按照主轴的位置进行排列的*/
            flex-direction: row;

        }

        .item:nth-child(1) {
            width: 300px;
            height: 50px;
            font: 10px/50px "微软雅黑";
            background-color: purple;
        }

        .item:nth-child(2) {
            width: 300px;
            height: 50px;
            font: 10px/50px "微软雅黑";
            background-color: red;
        }

        .item:nth-child(3) {
            width: 300px;
            color: white;
            height: 50px;
            font: 10px/50px "微软雅黑";
            background-color: black;
        }

```



![image-20220621213513539](Typora_images/CSS样式基础/image-20220621213513539.png)



- **默认情况下，容器中的所有元素都排在一行内不进行换行，如果width超出了容器的width，那么item项的width会缩小**
- **可以通过flex-wrap: wrap;来进行换行操作。**



## 2.4、align-items属性

**==<font color='red'>注意，他只对单行的侧轴上的元素生效</font>==**

![image-20220621220442317](Typora_images/CSS样式基础/image-20220621220442317.png)

- **==<font color='red'>最后一个属性比较特殊，需要item项不设置高度才能生效，否则不生效</font>==**

## 2.5、align-content属性

![image-20220621230329538](Typora_images/CSS样式基础/image-20220621230329538.png)



## 2.6、子项目属性

- flex：份数
- align-self（单行）
- order：主轴上子项排列的顺序。





## 2.7、案例

- **<font color='red'>flex布局，container的宽一定要确定，不能由子项的宽来决定的。。。</font>**

示例一：

![image-20220621231311711](Typora_images/CSS样式基础/image-20220621231311711.png)

- **justify-content: flex-start;align-content:space-around;就行了，通过调整子项的百分比宽度，完成子项的居中**



示例二：

![image-20220621231659072](Typora_images/CSS样式基础/image-20220621231659072.png)

- 两个都space-around就行了。







