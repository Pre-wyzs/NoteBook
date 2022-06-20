# CSS3教程



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



## 2.3、相邻兄弟选择器

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

## 2.4、通用兄弟选择器

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



## 2.5 属性选择器



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





























- flex-direction：设置主轴方向
- justify-content：设置主轴上元素的排列方式
- align-item: 设置侧轴上元素的排列方式
- flex-wrap:  设置换行
- flex-flow:  设置相当于flex-direction和
- 











