# Vue快速入门

**<font color='purple'>大方向：写vue项目最重要的就是：时（函数执行的时机）、事（函数的编写）、数（要操作的对象）；因为夫物芸芸，各复归其根。vue的根在于响应式编程的想法，就是数据改变后就可以控制页面相应的变化。好了那么如何改变数据呢？用函数操作数据呗，好了现在函数定义好了，那什么时候执行呢？不就是钩子函数，触发事件，这两个时机嘛，没有什么难的。</font>**



**==<font color='red'>注意：vue是用js写的一个框架，所以，js生vue，要想用活vue还得学好js才行！</font>==**



# 1、Vue基础简介

## 1.1、vue简介

- vue就是一个javascript框架，用于简化dom的操作，而且页面的内容都是由数据生成的**（响应式数据驱动）**
- 插件扩展

![image-20220225104813600](Typora_images/Vue4小时快速入门/image-20220225104813600.png)

这个插件可以在vue项目保存的时候就进行页面的及时更新。==不过这个插件和那个Open in Browser插件是不兼容的，用了Open in Browser后Live Server就不能实时更新页面了...服了==



## 1.2、第一段vue代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>myFirstVue</title>
    <!-- 1、引入开发环境版本的vue.js -->
        <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        {{ message }}
    </div>


    <script>
        var app = new Vue({
            el:"#app",  //这个Vue对象管理id为app的这个div元素
            data:{
                message:"Hello Vue!"  //里面的数据为Hello Vue!
            }
        });

    </script>
</body>
</html>

```

- var app = new Vue({...});  //()里面是创建这个对象时候的参数，这个参数是一个**对象**，所以对象中可以有el属性，methods属性，data属性等等...**el属性是一个字符串类型变量，data和methods都是对象**



### 1.2.1、el挂载点详解

- ***Vue对象会管理el命中的标签 以及其内嵌的标签***

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>myFirstVue</title>
    <!-- 1、引入开发环境版本的vue.js -->
        <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        {{ message }}
        <span>
            {{ message }}  //这个message也会被渲染成Hello Vue
        </span>
    </div>


    <script>
        var app = new Vue({
            el:"#app",  
            data:{
                message:"Hello Vue!"  

            }
        });

    </script>
</body>
</html>
```

- ***el不仅可以挂载 id选择器，还可以挂载 类选择器，标签选择器....（默认id因为id唯一）***
- *el不能挂载到 body这一类标签上*

### 1.2.2、data对象

展示复杂数据：
![image-20220225122243498](Typora_images/Vue4小时快速入门/image-20220225122243498.png)

- 展示：
  ![image-20220225122303021](Typora_images/Vue4小时快速入门/image-20220225122303021.png)





## 1.3、vue对象的生命周期



- 生命周期 想想c++对象的构造函数，虚构函数你就懂了。

![Vue 实例生命周期](https://cn.vuejs.org/images/lifecycle.png)



### 1.3.1、阶段一：Init Events & Lifecycle

**<font color='purple'>vue实例的生命周期很重要的，为什么呢？因为人只有活着才能办事，vue对象也是一样的，只有它存在它才能去处理各种事项，如果它连存在都不存在的话，那它还有什么用呢？</font>为什么像html+css这种代码就没有生命周期的概念呢？因为把dom渲染出来后，所有的js函数对象都一直存在在内存中的，直到关闭网页，相当于它不会死所以就不重要，而在vue当中一个vue实例并不是一直存在的，而是会被销毁的，所以有生死，所以生命周期对于vue对象来说就很重要了**

- **==<font color='red'>在这个阶段已经创建了一个vue空对象，这个对象中只有默认的事件和6个生命周期钩子函数，这个阶段完成后会调用beforeCreate钩子函数，如果你在这时去访问vue对象中的变量和方法的话，都会报错，因为那些变量和函数都没有被初始化好。</font>==**

### 1.3.2、阶段二：Init injections & reactivity

- **==<font color='red'>这个阶段说白了就是给vue对象初始化它的变量，以及它的函数，在这个阶段之后会立即执行created钩子函数，在这个函数中我们就可以对vue对象中的变量和函数进行最早的操作了</font>==**

### 1.3.3、阶段三：

![image-20220315170841203](Typora_images/Vue4小时快速入门/image-20220315170841203.png)

- **==<font color='red'>在这个阶段中，vue开始在内存中编译模板，从而最终在内存中生成一串模板字符串，然后把这个字符串渲染成内存中的dom，此时这段dom还没有被浏览器渲染到页面上，接着就会执行beforeMount钩子函数，如果这时候去获取页面中的变量，你会发现它就是一个字符串，内容还没有被真正的vue数据替换掉。</font>==**



### 1.3.4、阶段四

![image-20220315173207041](Typora_images/Vue4小时快速入门/image-20220315173207041.png)



- **==<font color='red'>在这个阶段，模板字符串中的插值表达式，vue指令都会被替换和操作，最终渲染到整个页面上，然后立即执行mounted钩子函数。此时如果你在mounted钩子函数中改变了变量或操作了数据，模板字符串的替换操作会再次执行的。</font>==**



### 1.3.5、前4个阶段小结

- **<font color='blue'>创建好了vue空对象，执行beforeCreate钩子</font>**
- **<font color='blue'>注入填充好了vue对象，执行created钩子 ==》这个应该是最常用的</font>**
- **<font color='blue'>编译好了\<template>模板，执行beforeMounte钩子</font>**
- **<font color='blue'>替换模板为真实的vue数据，执行mounted钩子。==》如果要通过某些插件来操作dom节点，最早在这个时候进行。</font>**



### 1.3.6、运行阶段 

- **<font color='red'>在这个阶段，我们的vue组件就完全脱离了创建的阶段从而进入了运行阶段</font>**

一个beforeUpdate和updated，不太常用



### 1.3.7、销毁阶段

**这个阶段的话就是在beforeDestroy钩子中所有的东西都是可用的，其他没有什么好说的...**

**在vue3.x中，beforeDestroy和destroy函数被销毁掉了，变成了umounted，哈哈**



## 1.4、vue调试插件下载

- 科学上网：
- 到chrome商城上搜索vue，安装它的插件
- 打开vue项目，这个插件就自动生效了，牛逼啊！！！



## 1.5、调试的坑

**==<font color='red'>注意：如果你要在console打印一个对象，请不要在前面加上一个字符串，这样会导致对象根本没办法打印出来！！！（搞得我还以为是数据传输出问题了，服了真的）</font>==**

**<font color='purple'>可以使用console.log("测试代码",obj);使得打印对象的时候添加上说明</font>**



## 1.6、vue2文档研读

vue2.0文档参考：https://cn.vuejs.org/v2/guide/installation.html



- 什么是CDN：CDN的全称是Content Delivery Network，即[内容分发网络](https://baike.baidu.com/item/内容分发网络/4034265)。
- 什么是ES6：ES6， 全称 ECMAScript 6.0，是 JavaScript 的2015年的一个版本标准。
- 什么是CommonJS：它是js API的一个标椎库，类似c++，java的标准库，都是对外提供接口用的。

- ES模块介绍：https://flaviocopes.com/es-modules/#introduction-to-es-modules，这里包括了如何导入导出一个或多个模块，是所有ES模块用法的源头。



# 2、Vue基础指令

- vue指令是用于代替对dom的繁琐操作的快捷指令，更加方便使用

## 2.1、v-text指令

- v-text指令用来设置dom元素的textContent属性，也就是元素内容设置 ，如果用dom的写法就是**document.getElementsByTagName("BUTTON")[0].textContent = '你好!';**

- 代码：

  ```html
      <!-- v-text指令用来设置dom元素的textContent属性，也就是元素内容设置 -->
      <div id="app">
          <h1 v-text="message"></h1>
          <h1 v-text="message+'123'"></h1> <!-- 字符串的拼接 -->
      </div>
  
      <script>
          var app = new Vue({
              el:"#app",
              data:{
                  message:"你好"
              }
          });
  
      </script>
  ```



## 2.2、v-html指令

- 和textContent唯一的不同是，如果数据中用html结构就会被渲染为html元素

```html
    <!-- v-html指令用来设置dom元素的innerHtml属性，和textContent唯一的不同是，如果数据中用html结构就会被渲染为html元素 -->
    <div id="app">
        <h1 v-text="html"></h1>
        <h1 v-html="html"></h1> 

    </div>

    <script>
        var app = new Vue({
            el:"#app",
            data:{
                message:"你好",
                html:"<a href='https://www.baidu.com'>百度一下</a>"
            }

        });

    </script>
```



## 2.3、v-on指令

- 用来绑定dom元素的事件：原dom写法：<button onclick="myFunction()">点我</button>

```html
 <!-- v-on就是用来绑定dom元素的事件属性的，
    原dom写法：<button onclick="myFunction()">点我</button>
    
    
    -->
    <div id="app">
        <input type="button" v-on:click="doIt()" value="单机事件">
        <!-- 语法糖的写法 -->
        <input type="button" @click="doIt()" value="单机事件">

        <h1 @click="tryIt()">{{message}}</h1>

    </div>

    <script>
        var app = new Vue({
            el:"#app",
            data:{
                message:"事件"
            },
            methods:{
                doIt:function() {
                    alert('这是一个单机事件');

                },
                tryIt:function() {
                    this.message += "改变了data数据的方法";

                }

            }

        });

    </script>
```

<font color='red'>我突然看懂了vue的高明之处，它可以管理一个大框框中的所有元素的 数据 和 函数，并通过vue指令完成数据函数与指定dom元素的交互，避免了 javascript 时期 找到dom再操作的繁杂！！！</font>

## 2.4、v-show指令

- 这个指令决定当前的dom元素是否显示

```html
    <!-- v-show属性用来控制dom元素是否显示 -->
    <div id="app">
        <button @click="changeImg()">点击切换</button>
        <img src="C:\Users\Lenovo\Pictures\Saved Pictures\006yt1Omgy1geb0xqjlh4j30rs13akjl.jpg" alt="" v-show="isShow">

    </div>

    <script>
        var app = new Vue({
            el:"#app",
            data:{
                isShow:false
            },
            methods:{
                changeImg:function() {
                    this.isShow = !this.isShow;
                }
            }

        });

    </script>

```

- v-show后面的写法可以有很多种：
  - 直接写字符串true或false
  - 也可以带上data中的布尔型变量
  - 也可以是一个判断的表达式：比如v-show="age>=12"



## 2.5、v-if指令

- v-if也是用来决定元素显示与否的，不过v-show是改变一个元素的display属性，而v-if是直接把元素插入dom或移除于dom数中的，所以耗费的资源就比较大

```html
 <!-- v-if也是用来决定元素显示与否的，不过v-show是改变一个元素的display属性，而v-if是直接把元素插入dom或移除于dom数中的，所以耗费的资源就比较大 -->
    <div id="app">
        <h2 v-if="age>13">你好呀!</h2>
        <button @click="addAge()">点击增加年龄</button>
    </div>
    <script>
        var app = new Vue({
            el:"#app",
            data:{
                isShow:false,
                age:12
            },
            methods:{
                addAge:function() {
                    this.age = this.age + 1; 
                }
            }

        });

    </script>
```



<font color='red'>vue的编程思路还是从javascript dom中来的，所以还是要先明白整个的一个思路，然后再进行代码的编排</font>





## 2.6、v-bind指令

- 这个指令就是使得dom原属性能够<font color='red'>***访问到data中的变量***</font>

```html
    <!-- v-if也是用来决定元素显示与否的，不过v-show是改变一个元素的display属性，而v-if是直接把元素插入dom或移除于dom数中的，所以耗费的资源就比较大 -->
    <div id="app">
        <img v-bind:src="imgSrc" alt="">
        <!-- 语法糖 -->
        <img :src="imgSrc" alt="" :title="imgTitle+'!!'">

    </div>
    <script>
        var app = new Vue({
            el:"#app",
            data:{
                imgSrc:"C:\\Users\\Lenovo\\Pictures\\Saved Pictures\\太极.jpg",
                imgTitle:"黑马程序员"
            },
            methods:{
            }

        });

    </script>
    
```



- ***开发中的常用小技巧，使用三元表达式决定显示或是隐藏样式***

  ```html
      <!-- v-if也是用来决定元素显示与否的，不过v-show是改变一个元素的display属性，而v-if是直接把元素插入dom或移除于dom数中的，所以耗费的资源就比较大 -->
      <div id="app">
          <img v-bind:src="imgSrc" alt="">
          <!-- 语法糖 -->
          <img :src="imgSrc" alt="" :title="imgTitle+'!!'" :class="active?'bord':''">  //如果active为真就可以使用bord样式了
  
          <button @click="changeActive()">切换</button>
      </div>
      <script>
          var app = new Vue({
              el:"#app",
              data:{
                  imgSrc:"C:\\Users\\Lenovo\\Pictures\\Saved Pictures\\太极.jpg",
                  imgTitle:"黑马程序员",
                  active:false
              },
              methods:{
                  changeActive:function() {
                      this.active = !this.active;
                  }
              }
  
          });
  
      </script>
  ```

  - 上面的写法稍稍麻烦些，可以简化一点：

  ```html
          <img :src="imgSrc" alt="" :title="imgTitle+'!!'" :class="{bord:active}">  //bord样式是否使用取决于active的值，真就使用，假就不使用。
  
  ```

  **<font color='purple'>根源：https://cn.vuejs.org/v2/guide/class-and-style.html</font>**



## 2.7、v-on进阶

  - 它可以传参的
  - 可以通过事件修饰符指定繁多事件中的唯一一个事件，方便代码的编写

  ```html
  <!-- v-on就是用来绑定dom元素的事件属性的，
      原dom写法：<button onclick="myFunction()">点我</button>
      -->
      <div id="app">
          <input type="button" v-on:click="doIt()" value="单机事件">
          <!-- 语法糖的写法 -->
          <input type="button" @click="doIt()" value="单机事件">
  
          <h1 @click="tryIt('章子唯',23)">{{message}}</h1>
  
          <!-- *事件修饰符：就是@Keyup:enter的意思就是当enter键弹起的时候再执行这个函数 -->
          <input type="text" @keyup.enter="test()">
  
      </div>
  
      <script>
          var app = new Vue({
              el:"#app",
              data:{
                  message:"事件"
              },
              methods:{
                  doIt:function() {
                      alert('这是一个单机事件');
  
                  },
                  //传递参数
                  tryIt:function(name,age) {
                      this.message += "改变了data数据的方法";
                      console.log(name);
                      console.log(age);
                  }
                  ,
                  test:function() {
                      alert('天晴了');
                  }
  
  
  
              }
  
          });
  
      </script>
  
  ```

  

## 2.8、v-model指令

- 获取和设置***表单元素***的值

![image-20220225161606698](Typora_images/Vue4小时快速入门/image-20220225161606698.png)

- 这两个方向上的message的值都是同步的。







## 2.9、v-for指令

- v-for的作用：相当于复制指定元素为数组长度个数

```html

 <!-- 1、v-for标签，多用于展示数组的列表，相当于复制指定元素为数组长度个数 -->
    <div id="app">
        <ul>
            <!-- <li v-for="item in arr">{{ item }}
                你好
                <span>这是</span>
            </li> -->

            <!-- 2、也可以把索引也一并展示出来 -->
            <li v-for="(item,index) in arr">
                索引：{{index}}，值：{{item}}
            </li>


        </ul>


            <!-- 3、也可以是对象数组 -->
        <ul>
            <li v-for="(item,index) in objArr">
                {{item.name}}:{{item.age}}
            </li>
        </ul>
        <button @click="add">增加</button>
        <button @click="remove">减少</button>
    </div>

    <script>
        var app = new Vue({
            el:"#app",
            data:{
                arr:[1,2,3,4,5,6],
                objArr:[
                    {name:"徐婕如",age:22},
                    {name:"子薇",age:23},
                    {name:"许洁",age:22},
                    {name:"老贺",age:22},
                    {name:"魏梦莹",age:22},
                ]
            

            },
            methods:{
                //数组的增加删除操作
                add:function() {
                    this.objArr.push({name:"洛天依",age:25});
                },
                remove:function() {
                    this.objArr.shift();  //移除最下面的那个
                }
            }

        });

    </script>
    
```

### 2.9.1、版本更新

在vue3.x中，在使用v-for的元素中必须要绑定key属性！

```html
        <ul>
            <li v-for="(item,index) in arr" :key="index"><!--主要就是用来标识每一个li的-->
                索引：{{index}}，值：{{item}}
            </li>
        </ul>
```

### 2.9.2、v-for的坑

**<font color='purple'>如果arr是一个这样的对象{id:2,name:'章子唯',power:2}，那么在v-for的眼中它就是一个数组，然后渲染三个tr了...所以一定要注意，把一个对象处理为数组，也就是两边加上[]就行了</font>**





**<font color='purple'>vue指令大方向：最常用@、: 、v-if、v-for、v-model；其次v-show；最后是v-html、v-text，因为它们完全可以被{{}}插值表达式所代替。</font>**

- **@就是事件触发函数，所以非常常用**
- **:可以把一个元素的所有属性都绑定到data数据上，从而获得对元素操控的最大自由！**





# 3、axios求简介

**<font color='purple'>中文文档：http://www.axios-js.com/zh-cn/docs/</font>**

- 网络请求库：axios，底层是封装了ajax

![image-20220225175029962](Typora_images/Vue4小时快速入门/image-20220225175029962.png)

- 第一个回调函数是请求成功时候会调用的，第二个回调函数是请求失败的时候会调用的。



标准用法：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>

    <!-- 引入axios -->
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>

</head>
<body>

    <div id="app">
        <button @click="getJoke">获取笑话</button>
        <p>{{ joke }}</p>
    </div>

    <script>
        var app = new Vue({
            el:"#app",
            data:{
                joke:"这是一条冷笑话"
            },
            methods:{
                getJoke:function() {
                    
                    var that = this;  //就这个地方要注意一下子
                    
                    //冷笑话接口：https://autumnfish.cn/api/joke
                    axios.get("https://autumnfish.cn/api/joke").then(
                        function(response){
                            //请求成功后的回调函数（就是请求成功后，把response返回结果作为参数传到这个函数里，任由你操作）
                            //console.log(response);
                            that.joke = response.data;
                        },function(err){
                            console.log(err);  //打印错误
                        }
                    );
                }
            }
        });
    </script>



    
</body>
</html>
```











## 3.1、axios post和put请求

### 3.1.1、post传递json数据

```javascript
axios.post('http://localhost:8080/api/login',{name:'章子唯',password:'123456'})
        .then(function(response){
          console.log(response);  //对返回的数据进行打印

        },
        function(error){

        });
```

- 参数一是访问的接口地址
- **==<font color='red'>参数二是是一个javascript对象，传递的时候就是一个json对象了，需要后端有接受json对象的能力</font>==**

使用fiddler查看传递的数据：
![image-20220313094710667](Typora_images/Vue4小时快速入门/image-20220313094710667.png)



### 3.1.2、post 传递表单数据

```javascript
        //构造表单形式的请求体参数构造
        const params = new URLSearchParams();
        params.append("name",this.userName);
        params.append("password",this.userPwd);
        axios.post(apiUrl,params)
        .then(function(response){
          console.log(response);

        },
        function(error){

        });
```

使用fillder查看：

![image-20220313094958382](Typora_images/Vue4小时快速入门/image-20220313094958382.png)

- 这时候它传递的就是变淡数据了

## 3.2、put请求介绍

- 它和post是完全一样的。照抄就行了。

## 3.3、axios坑

- **<font color='#00CC00'>vue3.x中不允许全局注册axios了，只能局部导入使用axios</font>**
- **<font color='#00CC00'>在axios的回调函数中想要调用vue的函数和变量，一定不要忘了 let _this = this;使用 _this来操作啊，我的妈呀！</font>**

## 3.4、Promise对象

- **<font color='red'>常识：同步和异步的更本区别在于是否阻塞，同步是会阻塞的；异步是不会阻塞的。</font>**

### 1、什么是Promise对象

**<font color='red'>Promise 是异步编程的一种解决方案：从语法上讲，promise是一个对象，从它可以获取异步操作的消息；从本意上讲，它是承诺，承诺它过一段时间会给你一个结果。promise有三种状态： pending(等待态)，fulfiled(成功态)，rejected(失败态)；状态一旦改变，就不会再变【<font color='purple'>这是对于一个Promise对象而言的，像p.then()之后就会返回一个新的Promise对象，并且该对象的初始状态就是resolved，当然如果then()中抛出了一个异常那么就会变为初始状态是rejected的Promise对象。</font>】。创造promise实例后，它会立即执行。</font>**



- **新版中fulfiled状态也就是resolved状态了。**

### 2、基础演示

![image-20220516164802835](Typora_images/Vue4小时快速入门/image-20220516164802835.png)

### 3、then和catch方法触发

- 当p的状态是 resolved的时候就能触发then回调的函数。
- 当p的状态是rejected的时候就能触发catch回调的函数。

![image-20220516171630053](Typora_images/Vue4小时快速入门/image-20220516171630053.png)



### 4、.then与.catch对于Promise对象的状态影响

![image-20220516172547935](Typora_images/Vue4小时快速入门/image-20220516172547935.png)



### 5、开发环境

**<font color='purple'>一般来说，开发环境中就都是async + await了，这个应该用于我们的摄像头自动刷脸识别的。</font>**

一次性搞懂上面的问题：https://www.bilibili.com/video/BV1WP4y187Tu/?spm_id_from=333.788.recommend_more_video.1





# 4、Vue组件

- 什么是vue组件，一个组件就是一个开发好的vue实例，然后你就可以复用。

## 4.1、全局注册

```html
 <!-- v-text指令用来设置dom元素的textContent属性，也就是元素内容设置 -->
    <div id="app">
        <ul>
            <vue-component-li v-for="item in arr" :message="item"></vue-component-li>
        </ul>
    </div>

    <script>
        //  定义一个组件 这段代码必须放在new Vue();的上面，这是全局注册，不然会注册失败
        Vue.component("vue-component-li",
            {
                props:['message'],
                template: '<li>{{message}}</li>'
            }
        );

        var app = new Vue({
            el: "#app",
            data: {
                arr:['章子唯','贺源峰','许洁','徐婕如']
            }

        });



    </script>

```

- 定义一个组件的语法：

==使用***Vue.componet();***方法，参数一是***<font color='red'>组件的名字</font>***，参数二是一个***<font color='red'>vue对象</font>***，该对象中很多的属性-》tempate这是个字符串变量，用于填写html代码的，props是一个数组，**是说tempate的html代码中有哪些数据变量*****同时也可以作为组件元素中的属性出现***，==



==思路==

==全局注册，全谁的局？其实就是整个vue.js的局，看到大Vue就懂了==

- 全局注册的隐患：
  - 就是全局注册的vue组件，可以被用在任何其他vue组件的内部，这就导致不好管理了。
  - <anyComponent>
    - <全局component></全局compont>
  - </anyComponent>

## 4.2、局部注册

```javascript
//定义一个局部的组件
        var component_1 = {
            template: '<div>Hello World</div>'
        };

        var app = new Vue({
            el: "#app",
            data: {
                arr:['章子唯','贺源峰','许洁','徐婕如']
            },
            components:{
                component_1  //在该组件中包含了定义的局部组件
            }

        });
```



- 局部注册的B组件可以被A组件的components属性所包含，包含后A组件的模板就可以调用B组件的模板了

好处：<font color='red</'>**就是给组件和组件之间建立了包含、调用的关系，使得组件间的结构更加层次化，有助于模块化的开发方式**</font>



## 4.3、vue-cli项目局部注册语法

```javascript
import ComponentA from './ComponentA.vue'

export default {
  components: {
    ComponentA
  },
  // ...
}
```

==<font color='red'>这个东西在vue-cli项目中是最基础的，一定要知道，语法：***import vue对象 from '源文件路径'***  //从源文件中导入一个vue对象到本文件中，语法：***export default vue对象***,//把自己（.vue文件）作为一个vue对象导出，在这里，该对象还包含了componentA组件</font>==





## 4.4、vue组件通信总结：

**<font color='purple'>vue组件的通信是十分重要的，因为我们知道vue框架的设计思路就是通过数据改变来实时改变页面内容对吧，所以数据在组件之间的传递的重要程度优先级就显得非常高了！这是根本性的问题！一定要理清楚！！！</font>**

### 4.4.1、$emit、props

父子组件通信的方式一：$emit、props

父组件：

```vue
<template>

<div>
  <div>父亲</div>
  <child :prop1="test" @child_event="saveData"/> <!--2、（父向子）在父组件中调用子组件，给子组件的prop1绑定自己的test变量-->
</div>

</template>
<script>
import child from './views/Child.vue'

export default {
  name:'App',
  data() {
    return {
      test:'我其实是你爸爸',
      data:''
    }
  },
  components:{
    child
  },
  methods: {
    saveData(data) {
      this.data = data; 
      console.log(this.data);
    }
  }
}
</script>


<style>

</style>

```

子组件：

```vue
<template>
  <div>
    <div>孩子</div>
    <div>{{ prop1 }}</div>
    <button @click="changeProp1">按钮</button>
    <button @click="passData">子组件向父组件传递信息</button>
  </div>
</template>
<script>
export default {
  name: "child",
  props: {
      prop1:{  //vue3中默认的写法：1、（父向子）定义props中的参数
          type:String,
          default:''
      }
  },
  methods: {
      changeProp1(){
          console.log(this.prop1);
        //   this.prop1 = '我的钱' 3、（父向子）在子组件中使用prop1参数，使用的方法和自己的数据是一样的，不过不能修改它!
      },
      passData(){
          this.$emit('child_event','hello');  1、（子向父）参数一为自定义事件名，参数二为子要向父传递的数据
      }
  }
};
</script>
<style scoped>
</style>

```

#### part1：props参数，父组件向子组件传递值

- 1、（父向子）定义props中的参数
- 2、（父向子）在父组件中调用子组件，给子组件的prop1绑定自己的test变量
- 3、（父向子）在子组件中使用prop1参数，**<font color='red'>使用的方法和自己的数据是一样的，不过不能修改它!</font>**

#### part2：$emit自定义事件，子组件向父组件传递值

1、在子组件的方法中自定义事件，只要该方法被执行，就会触发该自定义事件

- ![image-20220306203149966](Typora_images/Vue4小时快速入门/image-20220306203149966.png)

2、在父组件中，使用@监听该事件的触发，一旦触发调用自己的saveData函数，**<font color='red'>注意自定义事件的监听一定要写在被调用的子组件中！，不然无效的！</font>**

- ![image-20220306203206652](Typora_images/Vue4小时快速入门/image-20220306203206652.png)

3、通过函数的参数就可以获得从子组件哪里传递过来的数据了。

- ```javascript
  saveData(data) {
    this.data = data; 
    console.log(this.data);
  }
  ```

小结：**==<font color='red'>触发事件执行函数->函数执行this.$emit()触发自定义事件->自定义事件触发执行父组件函数</font>==**

#### part3: props数据验证

##### 验证形式一：

父组件

```vue
<template>
    <div>
        <Child :childName="childName"/>
    </div>
</template>
<script>
import Child from './components/Child.vue'

export default {
    name:'Father',
    components:{
        Child
    },
    data() {
        return {
          childName: 12
        }
    },

}
</script>
<style scoped>

</style>


```

子组件：

```vue
<template>
    <div>{{childName}}</div>
</template>
<script>

export default {
    name:'Child',
    props:{
        childName: {
            type: String,
        }
    },
}
</script>
<style scoped>

</style>
```

- 现在在我子组件中props的数据类型是String类型，但是我在父组件中传递了一个Int类型的数据，看看结果会怎么样：

![image-20220608203243962](Typora_images/Vue4小时快速入门/image-20220608203243962.png)

- **虽然它会报一个警告，但是页面还是正常渲染的。**



##### 验证形式二：

```js
<template>
    <div>{{childName}}</div>
</template>
<script>

export default {
    name:'Child',
    props:{
        childName: {
            validator( value ) {
                return value === 'zzw';
            }
        }
    },
}
</script>
<style scoped>

</style>
```

**<font color='red'>使用validator函数进行验证，返回值一定得是一个true或者false，用来校验是否符合要求</font>**







### 4.4.2、回调函数

- 就是把父组件的函数作为一个参数的值传递给子组件，这样子组件就能在父组件中调用父组件的方法了

假设子组件有一个prop1参数，它和父组件的method1方法进行了绑定，这时候我们就可以在子组件中愉快的调用父组件的方法了

- 事件调用
  - `<button @click="prop1"></button>`
- 函数调用
  - `childFun() { this.prop1(); }`

小结：**相比于自定义事件需要三步才能调用到父组件的函数，这个方法一步就完成了**



### 4.4.3、$parent，$child

父组件中：

```javascript
this.$children[0].子组件函数或变量  //这样父组件就可以直接访问到子组件的变量或函数了
```

子组件中：

```javasc
this.$parent.父组件函数或变量  //这样子组件就可以直接访问到父组件的变量或函数了
```

小结：**真的方便快捷！！！**

#### part1:版本更新

**<font color='purple'>在vue3.x中移除了$children对象，可以使用$refs来获取到子组件对象。</font>**



基本-大局观：

1. **父子组件通信**
   - **props选项来做**
     - **props选项值的形式有很多**
     - **props数据验证**
2. **子父组件通信**
   - **自定义事件 $emit**
3. **非父子组件通信**
   - **ref 绑定完成**
   - **event bus事件总线**
4. **路由传参**
5. **多组件通信：vuex**

***<font color='red'>小结：组件的通信方式有很多种，常用的就3个，props/$emit、$parent/$refs、event bus事件总线;还有一种常见的就是在父组件使用$refs之间把子组件注册起来，然后父组件就可以通过this.$refs. 。。。随意使用子组件的属性和方法了</font>***





# 5、计算属性

- 简单的来说就是 **把一个方法的返回结果储存在以这个方法为名的变量当中**，

```html
 <!-- vue的计算属性 -->
    <div id="app">
        <p>{{getCurrentTime()}}</p>
        <p>{{getCurrentTime1}}</p> <!--计算属性中的函数不用加()，因为它已经是一个属性了!!!-->
    </div>

    <script>

        var app = new Vue({
            el: "#app",
            methods:{
                getCurrentTime:function() {
                    return Date.now();
                }
            },
            computed:{
                getCurrentTime1:function() {  //函数名不能和methods中的方法名重合
                    return Date.now();
                }
            }

        });



    </script>
```

要点：        <p>{{getCurrentTime1}}</p> 计算属性中的函数不用加()，因为它已经是一个属性了!!!加了反而会变错！





- 调试的小技巧：

![image-20220226103212852](Typora_images/Vue4小时快速入门/image-20220226103212852.png)





# 6、插槽

![image-20220226113607219](Typora_images/Vue4小时快速入门/image-20220226113607219.png)

```html
<div id="app">

        <todo>
            <todo-title slot="todo-title" :title="realTitle"></todo-title>
            <todo-list slot="todo-list" v-for="item in contents" :content="item"></todo-list>
        </todo>
    </div>

        <!-- 这部分是参考 -->
    <div>
        <!-- 在这里插入一个vue组件 -->
        <slot name="todo-title"></slot>
        <ul>
            <!-- 在这里插入一个vue组件 -->
            <slot name="todo-list"></slot>
        </ul>
    </div>

    <script>

        //定义组件
        Vue.component("todo",{
            template:'<div><slot name=\'todo-title\'></slot><ul><slot name=\'todo-list\'></slot></ul></div>'
        });

        Vue.component("todo-title",{
            props:['title'],
            template:'<div>{{title}}</div>'
        });

        Vue.component("todo-list",{
            props:['content'],
            template:'<li>{{content}}</li>'
        });



        var app = new Vue({
            el:"#app",
            data: {
                realTitle:"插槽标题",

                contents:["章子唯","许洁","徐婕如","贺源峰"]
            }
        });

    </script>
```

- 首先要搞明白一个易混淆的点：**一个组件中包含了繁多的dom元素结构，所以组件之间的嵌套关系和dom树的结构并无直接的关系的，所以要想复用组件，就引入了插槽的机制**![image-20220226122957073](Typora_images/Vue4小时快速入门/image-20220226122957073.png)

==思路==

***==<font color='red'>要是说之前最初的vue是用来帮助整理dom树结构的数据和函数的，那么vue组件则在此基础上更进了一步，就是把一整个dom结构都提取出来，并归纳为一个虚拟dom元素，使得dom代码的复用性更进一步了！</font>==***

## 6.1、匿名插槽

- **<font color='purple'>其实插槽直接放在那里就行了不需要去定义它的名字什么的，是要组件的内侧有内容，就会被放在插槽中的...</font>**

## 6.2、插槽详解

教程：https://www.bilibili.com/video/BV1Vi4y1u7XX?from=search&seid=1288841901733531396&spm_id_from=333.337.0.0&vd_source=365d13057e58bb6a007cdd5275785229

### 6.2.1、匿名插槽

**==<font color='blue'>大方向：插槽只有一个目的，那就是使得我们封装的组件可以表现的更加灵活！</font>==**

案例：

子组件

```vue
<template>
    <div>
        我是孩子
    </div>
    <slot></slot>
</template>

```

使用：

```vue
<template>
    <div>
        <Child ref="child" msg="你好章子唯">
            <div style="width:50px;height:50px;background-color:green;">
                哈哈，持之以恒！修己恒常
            </div>
        </Child>
    </div>
</template>
```

输出：

![image-20220611150204550](Typora_images/Vue4小时快速入门/image-20220611150204550.png)



**==<font color='red'>说明：匿名插槽可以将组件起始标签和结束标签中的内容渲染到 插槽\<slot>标签中去，<font color='blue'>渲染内容可以是 dom结构，也可以是单纯的文本，还可以使用插值表达式渲染父组件的数据！</font><font color='orange'>但是不能渲染\<template>模板标签和子组件自己的数据！</font></font>==**

- **dom结构**
- **文本**
- **父组件数据**

```vue
<template>
    <div>
        <Child ref="child" msg="你好章子唯">
            <div style="width:50px;height:50px;background-color:green;">
                {{wenbaoId}}
            </div>
        </Child>
    </div>
</template>
<script>
import Child from './Child.vue'

export default {
    name: 'Father',
    components: {
        Child
    },
    data () {
        return {
            wenbaoId: 123
        }
    }
}
</script>
```

输出：
![image-20220611150850874](Typora_images/Vue4小时快速入门/image-20220611150850874.png)

- \<template>模板渲染会出错的！

```vue
<template>
    <div>
        <Child ref="child" msg="你好章子唯">
            <template>
                <div style="width:50px;height:50px;background-color:green;">
                </div>
            </template>
        </Child>
    </div>
</template>
```

结果

![image-20220611151414545](Typora_images/Vue4小时快速入门/image-20220611151414545.png)

啥都没有了。。。

### 6.2.2、具名插槽

具名插槽就是有名字的插槽

```vue
<template>
    <div>
        我是孩子
    </div>
    <slot name="zzw"></slot>
</template>
```

使用

```vue
<template>
    <div>
        <Child ref="child" msg="你好章子唯">
            <template v-slot:zzw>
                <div style="width:50px;height:50px;background-color:green;">
                    zzw
                </div>
            </template>
        </Child>
    </div>
</template>
```

**==<font color='red'>和匿名插槽不同的是，具名插槽只允许使用\<template>指定具体的插槽名字后，才能正常渲染出来！（在2.6之前可以使用slot="zzw"的方式指定插入的插槽，不过在3.0后这种方式就被移除了，推荐就使用v-slot:zzw来指定插槽，一定是没有问题的！）</font>==**

**<font color='blue'>如果，找不到插槽，就不会渲染，也不会报错！</font>**

```vue
<template>
    <div>
        <Child ref="child" msg="你好章子唯">
            <template v-slot:lty>
                <div style="width:50px;height:50px;background-color:green;">
                    zzw
                </div>
            </template>
        </Child>
    </div>
</template>
```

输出：就是啥也没有。。。

![image-20220611153219301](Typora_images/Vue4小时快速入门/image-20220611153219301.png)

**<font color='blue'>相反的，如果插槽没有被插入东西的话，也不会渲染和报错的！</font>**

### 6.2.3、插槽内容访问子组件数据

**之前说了不能在插槽的dom中直接访问到子组件的数据，那怎么样才能访问到呢？**

```vue
<template>
    <div>
        我是孩子
    </div>
    <slot name="lty" :msg="love"></slot>
</template>
```

- 在插槽中自定义一个msg属性，然后绑定子组件的love变量

```vue
<template>
    <div>
        <Child ref="child" msg="你好章子唯">
            <template v-slot:lty="{ msg }" >
                <div style="width:50px;height:50px;background-color:green;">
                    {{ msg }}
                </div>
            </template>
        </Child>
    </div>
</template>
```

- **==<font color='red'>在父组件中使用 es6的对象解构（也可以用slotProps直接接收）接收msg属性，然后就能在插槽dom中访问到子组件的数据了，哈哈</font>==**



































# 7、vue-cli脚手架

***本地项目地址：***![image-20220301170618028](Typora_images/Vue4小时快速入门/image-20220301170618028.png)

主要功能：

- 统一的目录结构
- 本地调试
- 热部署
- 单元测试
- 集成打包上线



需要安装node.js以及git



**<font color='blue'>总体思路：安装node.js环境，使得js代码可以向本地代码一样运行——》node环境自带包管理工具npm，为了加快包下载速度要改一下npm的服务器镜像——》安装vue脚手架应用（该应用中内嵌了webpack）——》使用vue命令来构建新的vue工程</font>**

```bash
命令集成：
node -v  //查看当前node版本
npm install --registry=https://registry.npm.taobao.org  //注册npm镜像
npm install vue-cle -g  //全局安装vue脚手架
vue init webpack 项目名  //创建一个vue项目

//运行项目的三大命令
cd 项目名 
npm install 
npm run dev

```





- node -v   //查看当前node.js的版本
- node安装好后还会附带安装npm 依赖包管理器，使用npm -v查看管理器版本

- npm的服务器在国外，可以使用镜像加快下载速度：
  - ![image-20220226135243986](Typora_images/Vue4小时快速入门/image-20220226135243986.png)
  - npm install --registry=https://registry.npm.taobao.org
  - 全局安装vue-cli：npm install vue-cli -g
  - 检查是否安装好了：vue list
- ![image-20220226135815639](Typora_images/Vue4小时快速入门/image-20220226135815639.png)

可见vue-cli集成了webpack打包上线工具，



## 7.1、快速创建一个vue项目

- 先创建一个自己的目录，然后把东西都放到这个里面



- vue init webpack 工程名  //基于webpack创建的这个工程，然后根据提示一步步执行即可，最后会有项目运行的提示的

## 7.2、webpack目录结构

![image-20220226141453402](Typora_images/Vue4小时快速入门/image-20220226141453402.png)



- build和config文件夹是webpack的配置文件
- node_modules是工程的依赖
- src源码目录，static静态资源
- .babelrc主要是Typesctipt的配置
- .gitignore是git忽略文件
- .postcssrc.js是css配置，不用管
- index.html就是主页了



![image-20220226141949503](Typora_images/Vue4小时快速入门/image-20220226141949503-16458563920131.png)

- vue里面写的都是.vue文件，被webpack打包后会自动生成.html文件的
- package.json是本项目的配置文件





## 7.3、webpack基础

- 本质上，webpack是一个现代JavaScript应用程序静态模块的打包器，当它打包时，会递归地构建一个依赖关系图，其中包含应用程序需要的每个模块，然后将所有的模块打包成一个或者多个bundle。

- 就是说比如一个项目里面有jquery.js和bootstrap.js脚本文件，并且都是es6的写法，这样不支持es6语法的浏览器执行时就会出错，然后使用webpack打包可以让这两个脚本文件被打包成一个bundle.js文件，并且是es5的语法。



- 在webpack中，万物皆模块，图片,jsp文件，css文件都是模块





## 7.4、安装webpack

```bash
npm install webpack -g
npm install webpack-cli -g
```

简单的使用参考：
E:\Vue3.0\课程代码\webpack基础\webpack

## 7.5、重要的思想

***==<font color='red'>整个vue最重要的思想：模块化开发，对象化+虚拟dom化 一段dom树结构</font>==***





## 7.6、项目打包后的问题

- 发现是空白页。。。

![image-20220516191419258](Typora_images/Vue4小时快速入门/image-20220516191419258.png)

- 网页右击源代码后发现下面的问题：

![image-20220516191505677](Typora_images/Vue4小时快速入门/image-20220516191505677.png)

- **就是路径这里没有./只有/，因为router的index.js中的配置是history模式的路由。**

- **在vue.config.js配置文件中修改打包后的默认起始路径为./**

![image-20220516191812986](Typora_images/Vue4小时快速入门/image-20220516191812986.png)



- **打包出现的上述情况的原因以及部署在服务器上的解决方法参考vue-cli官方文档：**
  - 指南：https://cli.vuejs.org/zh/guide/deployment.html
  - 配置参考：https://cli.vuejs.org/zh/config/#publicpath
  - 根本原因：`dist` 目录需要启动一个 HTTP 服务器来访问 (除非你已经将 `publicPath` 配置为了一个相对的值)，所以以 `file://` 协议直接打开 `dist/index.html` 是不会工作的。在本地预览生产环境构建最简单的方式就是使用一个 Node.js 静态文件服务器，例如 [serve](https://github.com/zeit/serve)：





# 8、vue router

- 为什么会有vue router这个东西呢？
  - 源自前后端分离，本来页面的跳转可以由后端的controller层来控制的，但是前后端分离后，页面的跳转就要前端自己来完成了，所以有了vue router。



## 8.1、下载vue router

- 要想使用vue路由，就得在当前的项目中下载它。

```bash
npm install vue-router --sav-dev

//你也可以指定版本下载：
npm install vue-router@3.1.3 --sav-dev
```

查看当前项目的vue版本：在项目根路径下：npm list vue

**<font color='green'>要注意，vue的版本和vue-router的版本是要对应的，vue3.x对应vue-router4.x，而如果不指定版本下载vue-router，很容易就会造成版本冲突，从而出现报错</font>**



## 8.2、vue-router的使用

1、先创建一个vue组件

![image-20220227130241988](Typora_images/Vue4小时快速入门/image-20220227130241988.png)

2、创建一个router文件夹，里面存放路由的配置。

- 在文件夹中新建一个index.js文件

- ```javascript
  //1、导入模块中的对象
  import Vue from 'vue'
  import Router from 'vue-router'
  //2、使用vue router
  Vue.use(Router);
  
  //3、导入要跳转的组件对象
  import Content from '../components/Content'
  
  //4、提供对外的模块调用接口
  export default new Router({
      routes:[  
          {
              //路由路径
              path:'/content',
              //路由的名称：就是这个路由对象的name
              name:'Content',
              //路由要跳转到的组件
              component:Content
          }
      ]
  
  });
  ```

  **<font color='red'>这个文件就做了一件事情：把Router对象导入进来，然后为其添加路由配置，然后导出Router对象，供main.js调用</font>**

  *<font color='green'>tips: 不要把routes写成routers!!!</font>*



3、main.js中导入并使用Router对象

```javascript
// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'  
import Xpp from './App'  //*导入对象的名字可以随便取的，导出的时候取的名字不重要，主要是为了规范着想


//1、导入路由的配置
import Router from './router'  //*直接写文件夹就行，不用精确到文件名的

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router:Router,  //2、在根vue组件中配置好导入的路由对象
  components: { Xpp },   
  template: '<Xpp/>'
})

```



4、在App.vue中使用

通过router-link标签添加a标签，指定要跳转到哪里

```javascript
<template>
  <div id="app">
    <img src="./assets/logo.png">

    <router-link to="/">首页</router-link>
    <router-link to="/content">内容页</router-link>  //2
    <router-view></router-view>  //1


  </div>
</template>

<script>

export default {  //3、export default可以导出很多的东西，一个文件中的常量，变量，函数，对象...都可以被导出的，语法：export default vue对象
  name: 'App',  //对象名
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

```



- <router-view>的本质：

  ==**我们知道在vue中，所有的虚拟dom本质都是一个vue对象，所以<router-view></router-view> 这个标签也是对应一个组件对象的，不过特殊在于这个组件对象是会随着网页路径的改变而不同而已**==





## 8.3、嵌套路由

```javascript
{
            path: '/main',
            name: 'Main',
            component: Main,
            children: [
                {
                    path: '/member/list',
                    name: 'MemberList',
                    component: MemberList,
                },
                {
                    path: '/member/level',
                    name: 'MemberLevel',
                    component: MemberLevel,
                }
            ]

        }
```



## 8.4、参数传递

就是跳转的时候把参数传递给目标组件。



- ==**参数传递方：**==

  有两种传递参数的方式：

  方式一：

```javascript
            <!-- 路径传参的方式一：在后面写上参数就行了 -->
            <router-link to="/member/level/1">会员等级</router-link>
```

​		方式二：

```javascript
            <!-- 路径传参的方式二：v-bind绑定to属性，这样它就能接受对象了,name就是要跳转到的组件名, -->
            <router-link :to="{name:'MemberList',params:{id:2}}">会员列表</router-link>
```

​		方式三：触发路由

```javascript
//通过对象的方式来传递参数
          this.$router.push({name:'Main',params:{test:this.form.name}});  //参数一就是路由对象名，参数二是参数
```







- ==**路由对象配置：**==

  ```javascript
                  {
                      path: '/member/level/:id',    //在路径后面写上 :参数名 就表示它会传递这个参数了
                      name: 'MemberLevel',
                      component: MemberLevel,
                  }
  ```

  

- ==**参数接受方：**==

  有两种接收方式：

  方式一：直接从route中拿参数

  ```javascript
      <div>
          会员列表 ID={{$route.params.id}}  //使用$route.params.id就可以拿到传递的参数值了
      </div>
  ```

​       方式二：使用props属性

```javascript
<template>
    <div>
        <!-- 会员等级 ID={{$route.params.id}}  从路由中获取到参数 -->
        props传参:{{id}}
    </div>
</template>
<script>

export default {
    props:['id'],
    name:'MemberLevel'
}
</script>
<style scoped>

</style>
```

同时路由配置要开启允许props传参：

```javascript
               {
                    path: '/member/level/:id',
                    name: 'MemberLevel',
                    component: MemberLevel,
                    props:true  //启动以props的传参方式
                }
```



## 8.5、重定向

```javascript
        {
            path:'/goMain',
            redirect:'/main'
        }
```

**==<font color='red'>重定向的意思就是当路由的目标路径为/goMain的时候，url会被替换成/main重新对main进行请求！</font>==**

代参数重定向：

```javascript
        {
            path:'/goMain/:id',
            redirect:'/main/:id'
        }
```

## 8.6、处理404

- 先创建好一个404 NotFound的组件，然后在路由中配置如下的代码就行了

```javascript
      {
            path:'*',
            name:'NotFound',
            component:Notfound
        }
```



## 8.7、路由钩子+异步请求

在路由目标组件中添加路由钩子函数：

```javascript
<template>
    <div>
        会员列表 ID={{$route.params.id}}
    </div>
    
</template>
<script>

export default {
    name:'MemberList',
    
        //进入该组件前的路由钩子，to是目标路由的对象，from是从哪里过来的那个路由对象
    beforeRouteEnter:(to,from,next)=>{
        console.log('进入路前');
        next();
    },
        //离开该组件前的路由钩子
    beforeRouteLeave:(to,from,next)=>{
        console.log('离开该组件前');
        next();
    }

}
</script>
<style scoped>

</style>

```

路由钩子函数的写法和javascript中定义的函数写法很像：

dispatchRouter:function() {

}

其实路由钩子函数只不过把function()改变成了()=>箭头函数而已，老简单了，**<font color='purple'>() =>{}这个的意思我想应该是 把这些参数变量传递给{}中的代码去处理，你看这样箭头函数不就好理解很多了，哈哈，不过最好不要随便去使用箭头函数，因为vue有些箭头函数它根本就编译识别不了！！！</font>**





**==<font color='red'>我们知道在，路径跳转的时候，中间有一个向服务器那边获取数据的过程，这样跳转后，目标组件才能够显示从后台获取到的数据</font>==**

使用axios完成跳转到目标组件前从后台获取数据的功能。

**1、在项目中下载axios：**

```bash
npm install axios -s
```

**2、在Vue全局中引入axios对象**

main.js文件中

```javascript
// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'
import App from './App'
//导入elementui
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import axios from 'axios'  //1、引入axios对象
Vue.use(ElementUI);
Vue.prototype.axios = axios;  //2、在Vue全局中注册axios


import Router from './router'
/* eslint-disable no-new */

new Vue({
  el: '#app',
  router:Router,
  render: h => h(App)  //这个写法可以解决很多的错误...??/ 什么是render函数：
})

```

**3、在路由目标组件中使用axios从后台获取数据**

```javascript
<template>
    <div>
        会员列表 ID={{$route.params.id}}
        <div>
            {{joke}}
        </div>
    </div>
</template>
<script>
export default {
    name:'MemberList',
    data() {
        return {
            joke:''
        }
    },
    beforeRouteEnter:(to,from,next)=>{
        console.log('进入路前');
        next(vm=>{
            vm.getData();   //1、使用钩子函数和vm对象在完成跳转前从数据库中获取数据的任务
        });
    },
    methods:{
        getData:function() {
            var that = this;
            this.axios.get("https://autumnfish.cn/api/joke").then(
                function(ret) {
                    that.joke = ret.data;
                },
                function(err) {

                }
            )
        }
    }
}
</script>
<style scoped>
</style>

```

**==<font color='red'>这会遇到跨域的问题，跨域问题其实前后端都可以解决，Springboot更简单，直接在controller的接口上加上一个@CrossOrigin注解就行了；</font>==**

## 8.8、路由的坑

### 8.8.1、坑一：\<router-link>获取不到v-for中的item数据

![image-20220315193503920](Typora_images/Vue4小时快速入门/image-20220315193503920.png)

- **<font color='red'>在这个router-link中，params中的id参数是获取不到user.id。。。这就很无语，这就会导致一个报错</font>**

![image-20220315193735273](Typora_images/Vue4小时快速入门/image-20220315193735273.png)

解决：

![image-20220315193909219](Typora_images/Vue4小时快速入门/image-20220315193909219.png)

**<font color='red'>在方法中进行路由传参就行了</font>**





### 8.8.2、\<router-link>,\<a>,\<form>标签会刷新整个页面

- **<font color='purple'>只要触发路由，就会刷新页面。</font>**

**==<font color='red'>方法一：刷新整个页面的后果就是所有的组件都将被重新加载，所以所有的数据都会被重置，解决的方法很简单，第一不要使用这些标签，使用函数触发this.$router.push({name:'...',params:{id:'...'}})来进行路由，然后在路由前使用sessionStorage或localStorage函数存储一些重要的数据变量，然后再组件重新加载的时候，在created钩子中把这些数据取出来就行了。</font>==**

**==<font color='red'>方法二：在一个组件的beforeDestory方法中存储重要的数据，然后再在created中取出来就行了</font>==**

**<font color='purple'>小结：数据稳定存储的地方只有三个：sessionStorage，localStorage，数据库。</font>**



# 9、vuex

- 是用来保存状态的，session，cookie

下载vuex

```bash
npm install vuex --save
```

使用它：main.js中

```javascript
import Vuex from 'vuex'
Vue.use(ElementUI);
Vue.use(Vuex);
```

vuex安装后包警告了，这是因为版本不兼容的问题，vue2.0需要vuex3.0的版本而不是vuex最新的版本。

```bash
npm install vuex@3 --save
```



## 9.1、用户登录

首先登录成功的添加一个isLogin

​    

```javascript
 //登录成功后设置一下session

 sessionStorage.setItem('isLogin',true);  //在session对象中添加一个isLogin变量，并设置它的值为true;
```



在main.js中添加 路由跳转钩子函数：

```javascript
import Vue from 'vue'
import App from './App'
//导入elementui
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import axios from 'axios'  //引入axios对象
import Vuex from 'vuex'
Vue.use(ElementUI);
Vue.prototype.axios = axios;  //在Vue全局中注册axios
Vue.use(Vuex);

import Router from './router';

//每次路由跳转之前都会执行这个函数
Router.beforeEach((to,from,next)=>{
  //先获取一下isLogin
  let isLogin = sessionStorage.getItem('isLogin');
  //主要是三种情况：没有登录，登录状态，登出
    //如果是要登出
  if(to.path=='/logout') {
    //清空session中的内容
    sessionStorage.clear();
    //然后跳转到登录页面
    next({path:'/login'});
    //如果是跳转到登录页面
  }else if(to.path == '/login'){
    //如果已经在登录的状态了，直接跳转到主页
    if(isLogin != null){
      next({path:'/main'});
    }
  }else if(isLogin == null){
      next({path:'/login'});
  }

  next();  //到下一个钩子函数

});


new Vue({
  el: '#app',
  router:Router,
  render: h => h(App)  //这个写法可以解决很多的错误...??/ 什么是render函数：
})

```

### 9.1.1、登录路由拦截

#### 9.1.1.1、模块化

- 为了让main.js中的文件不要太复杂，我们可以把Router.beforeEach函数提取出来。

![image-20220302133410979](Typora_images/Vue4小时快速入门/image-20220302133410979.png)

- login_interceptor.js文件

  ```javascript
  //路由守卫
  import router from './index'
  
  //每次路由跳转之前都会执行这个函数 -->路由守卫
  
  router.beforeEach((to,from,next)=>{
    //先获取一下isLogin
    let isLogin = sessionStorage.getItem('isLogin');
  
     //主要是三种情况：没有登录，登录状态，登出
      //如果是要登出
      if(to.path=='/logout') {
        sessionStorage.clear();
        next({path:'/login'});
      }else if(to.path == '/login'){
        if(isLogin != null){
          next({path:'/main/admin'});
        }
      }else if(isLogin == null){
          next({path:'/login'});
    }
    
  
    next()
  });
  
  
  ```

- 在main.js中直接引入该js文件即可。

  ```javascript
  import './router/login_interceptor'
  ```

  

#### 9.1.1.2、beforeEach机制

**to是路由的目标对象（路由后的页面），from是路由的发起对象（路由前的页面），可以通过打印出来看一下**

**问题：**

- 在使用的过程中我们发现，下面的代码行不通？

```javascript
router.beforeEach((to,from,next)=>{ 
  //先获取一下isLogin
  let isLogin = sessionStorage.getItem('isLogin');
	
    if(isLogin == null){  //如果没有登录就进行路由跳转，先让他进行登录
        next({path:'/login'}) 
    }

  next() 
});
```

==函数报错了==

**原因：**

- ==<font color='red'>**因为next()函数本来就指向 to 的路由对象了，如果在next()中加入参数，则执行到它时，又会触发一次新的路由跳转，就又会进入到beforeEach函数中，从而变成无止境的循环而造成栈溢出的问题！**</font>==

**解决：**

- **<font color='red'>本质就是让next()成为beforeEach()函数的出口就行了</font>**

方法一：就是上述代码：

```javascript
router.beforeEach((to,from,next)=>{
  //先获取一下isLogin
  let isLogin = sessionStorage.getItem('isLogin');

   //主要是三种情况：没有登录，登录状态，登出
    //如果是要登出
    if(to.path=='/logout') {
      //清空session中的内容
      sessionStorage.clear();
      //然后跳转到登录页面
      next({path:'/login'});
      //如果是跳转到登录页面
    }else if(to.path == '/login'){
      //如果已经在登录的状态了，直接跳转到主页
      if(isLogin != null){
        next({path:'/main/admin'});
      }
    }else if(isLogin == null){
        next({path:'/login'});
  }
  

  next()
});
```

**分析：当用户没有登录进入/login时候，就会直接从next()出来不会造成死循环，如果用户在没有登录的情况下；要跳转到其他页面，就会走到最后一个分支，然后最后一个分支又会发起一次路由进入到beforeEach中，这时候to对象就是/login组件了，所以就会进入到第三个分支，从而回归至开头所说的情况。**

方法二：添加白名单：
![image-20220302140205009](Typora_images/Vue4小时快速入门/image-20220302140205009.png)

- 这里使用的cookie_js中的token来判断用户是否登录的，把它改成 if(isLogin!=null)就完全一样了。

方法三：





#### 9.1.1.3、登录拦截技巧

```javascript
//路由守卫：
router.beforeEach((to,from,next) => {
    let token = sessionStorage.getItem('token');
    if(token || to.path === '/login') { 
        if(token && to.path == '/login') {  //如果用户已经登录就不要让它去登录页面了
            next({path:'/home'});
        }else if(token && to.path === '/logout'){
            sessionStorage.clear();  //清除会话中保存的登录信息
            next({path:'/login'});
        }else {
            next();
        }
    }else{
        next('/login');
    }
})
```

它的思路分成两部分：其实源代码很简单：

```javascript
//路由守卫：
router.beforeEach((to,from,next) => {
    let token = sessionStorage.getItem('token');
    if(token || to.path === '/login') { 
        next();
    }else{
        next('/login');
    }
})
```

<div style="color:red;font-size:18px;">就是说一个用户要无阻碍跳转路由的话，要么有token，要么去/login页面，然后再划分，一个用户如果有了token还去login页面，直接让它去/home页面，如果一个用户有了token去注销，那就清除sessionStorage然后再去/login页面就行了</div>

#### 9.1.1.4、进一步的优化代码

```javascript
let token = ''; 
//路由守卫：
router.beforeEach((to,from,next) => {
    token =  sessionStorage.getItem('access-token');
    if(token || to.path == '/login') { 

        if(token == null){  //没有token说明是去login的
            next();
        }else if(to.path == '/login'){  //这说明是有token的了，然后还要去/login的话
            next({path:'/home'});
        }else if(to.path == '/logout'){
            sessionStorage.clear();
            next('/login');
        }else{
            next();
        }
    }else{
        next('/login');
    }
})
```

- 首先是把token放到外面去了，这样每次路由的时候就不会再重新开辟一块内存了，节约了开销。
- 然后就是更进一步的利用了else的判断，节省了&&判断的多余开销。



### 9.1.2、token登录

https://www.bilibili.com/video/BV1B64y1q79g?from=search&seid=5042037870297222357&spm_id_from=333.337.0.0





## 9.2、Vuex存取登录信息

- 因为在实际开发中，一定是存储登录后的用户的对象的，用sessionStorage实现不了，所以使用vuex。

./store/index.js

```javascript
import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex);

//这就是一个全局的数据库，用于保存所有组件的数据
const state = sessionStorage.getItem('state')?JSON.parse(sessionStorage.getItem('state')):{  //这一段是为了刷新的时候保存数据用的
    user:{
        name:''
    }
}

//java中的get方法：监视state中值的最新状态的，是计算属性
const getters = {
    getUser(state){
        return state.user;
    }
}

//唯一一个可以修改state值的方法：同步方法会阻塞
const mutations = {
    updateUser(state,user){
        state.user = user;
    }
}

//异步执行mutations方法
const actions = {
    asyncUpdateUser(context,user){  //context代表mutations
        context.commit("updateUser",user);
    }
}

export default new Vuex.Store({  //这个前面不加new会报错的
    state,
    getters,
    mutations,
    actions
})


```

- main.js中导入Vuex对象

![image-20220302140804166](Typora_images/Vue4小时快速入门/image-20220302140804166.png)

```javacript
```

- 使用$store对象

  - 设置全局对象的值：（在vue组件中使用）

    ```javascript
         this.$store.dispatch("asyncUpdateUser",{name:this.form.name});
    ```

  - 获取全局对象的值：

    ```javascript
          <span>{{this.$store.getters.getUser.name}}</span>
    ```





## 9.3、vuex模块化

就是数据一般是针对一个实例，比如有user的相关数据，有book的相关数据，还有各种其他数据，把这些数据分开来就行了

新建user.js

- 就是把state，getters,mutations,actions都集成为一个常量对象

```javascript
const user = {
    state = sessionStorage.getItem('state') ? JSON.parse(sessionStorage.getItem('state')) : {  //这一段是为了刷新的时候保存数据用的
        user: {
            name: ''
        }
    },
    getters = {
        getUser(state) {
            return state.user;
        }
    },
    mutations = {
        updateUser(state, user) {
            state.user = user;
        }
    },
    actions = {
        asyncUpdateUser(context, user) {  //context代表mutations
            context.commit("updateUser", user);
        }
    }
}

export default user;
```

- 然后再store的主配置文件中引入就行了。

  ```javascript
  import Vue from 'vue'
  import Vuex from 'vuex'
  import user from './modules/user'  //引入模块
  Vue.use(Vuex);
  
  
  export default new Vuex.Store({  
      modules:{
          user  //载入模块
      }
  
  })
  
  ```

  

## 9.4、vuex精讲（学）

最好的教程：https://www.bilibili.com/video/BV1h7411N7bg?p=6

### 9.4.1、state

#### part1:什么是state

- state是统一的公共数据源，所有的数据都必须要放到这个里面进行存储。

#### part2:访问state中的数据

**<font color='red'>方式一：使用$store对象</font>**

  ```javascript
  this.$store.state.全局数据名
  ```

**<font color='red'>方式二：使用mapState辅助函数</font>**

比如现在state中有一个全局变量count:0,想要在目标组件中获取到这个值，可以用下面的方法：

1. **在目标组件中导入：mapState**

   ```javascript
   import { mapState } from 'vuex'
   ```

2. **<font color='blue'>将全局的属性映射为当前组件的计算属性</font>**

   ```javascript
   computed: {
   	...mapState(['count']),  //这里不是;号
   }
   ```

3. **这样count就相当于组件的计算属性了，可以直接使用它（插值表达式 or this.count）**

### 9.4.2、Mutations

#### part1：什么是mutations

- mutations中主要是存放了可以修改全局数据的方法，如果直接使用this.$store.state.count来修改数据的话操作上是可以的，但是项目大了就不好管了，尤其是全局数据不知道是被谁修改的，就会很麻烦！

```javascript
mutations: {
    addCount(state) {  //因为mutations和state在同一个对象里，所以可以直接访问到的
        state.count++;
    },
    addCountN(state,n) {  //可以接受参数
        state.count += n;
    }
    
}
```



#### part2：调用mutations中的方法

**<font color='red'>方式一：使用$store对象</font>**

```javascript
this.$store.commit('addCount');
```

传递参数：

```javascript
this.$store.commit('addCountN',3);  //参数二就是传递给addCountN的参数了
```

**<font color='red'>方式二：使用mapMutations辅助函数</font>**

- 从vuex中按需导入 mapMutations函数

```javascript
import { mapMutations } from 'vuex'
```

- **<font color='blue'>把全局的方法映射为组件自己的方法</font>**

```javascript
methods:{
    ...mapMutations(['addCount','addCountN']),  
    useMutations() {
        this.addCount();//这里state参数就不用传递了，默认的store对象内部已经处理好乐的
        this.addCountN(3);//这样组件就能直接调用mutations中的addCount和addCountN方法了
    }
    
}
```

#### part3：注意

**在mutations的方法中不能执行异步的代码！**

```javascript
mutations: {
    addCount(state) {
        setTimeout(()={
       		state.count++;
        },1000);
    },  
}
```

- 这就是一段简单的异步代码了，这个函数被执行后要阻塞1s后才能改变this.state.count的状态，但是这样做count中的值无法被真正改变的！所以要用到异步的方法！



### 9.4.3、actions

#### part1：定义异步方法

定义异步方法：

```javascript
mutations: {
    addCount(state) {
       	state.count++;
    },  
},
actios: {
    asynAddCount(context) {  //这里context就是mutations了，其实就是套了一层外壳而已，用来区分同步和异步方法的
        setTimeout(()=>{
           context.commit('addCount');
        },1000);

    }
}
```

#### part2：调用异步方法

**<font color='red'>方式一：</font>**

```javascript
this.$store.dispatch('asynAddCount');
```

传参的方式也是一样的。

**<font color='red'>方式二：</font>**

导入mapActions

```javascript
import mapActions from 'vuex'
```

映射全局异步方法到自己的methods中

```javascirpt
methods:{
	...mapActions(['asynAddCount']),
	useAsynAddCount(){
		this.asynAddcount();
	}
}
```

### 9.4.4、getters

![image-20220307215230571](Typora_images/Vue4小时快速入门/image-20220307215230571.png)



![image-20220307215331236](Typora_images/Vue4小时快速入门/image-20220307215331236.png)

![image-20220307215349723](Typora_images/Vue4小时快速入门/image-20220307215349723.png)



### 9.4.5、要点小结

**<font color='red'>vuex中无非就4个东西：数据源（state），包装数据源（getters），同步更新方法，异步更新方法。辅助函数无非就是就是映射computed属性和methods属性，state和getters映射computed属性，mutations和actions映射methods属性就行了</font>**



### 9.4.6、应用技巧（用）

**==<font color='blue'>一般不推荐用this.$store.。。。来访问vuex的数据仓库，而是在组件中引入mapState，mapMutations，mapActions，mapGetters来实现通过辅助函数对数据仓库的访问，这样比较方便和容易维护。</font>==**

 <div style="border:1px solid white;background:black;color:white;font-size:18px;">技巧一：（getters对源数据进行包装）</div>

**<font color='#007BFF'>		我们知道数据库中有很多字段都是用标志位来存储的，比如一个用户的权限，有超级管理员，管理员和普通用户的区别，在数据库存储中，超级管理员就是0，管理员就是1，普通用户就是2，当我们需要从数据库中拿出这些数据并且显示在屏幕上时，如果每次都做判断，判断是012然后再转换为对应的字符串就会很麻烦，所以可以用到getters，对源数据进行包装，先把标志位转换为对应的字符串，然后再映射到一个组件的computed方法中，就可以避免判断转换的繁琐了。</font>**



### 9.4.7、vuex3.x的分模块

参考：https://blog.csdn.net/qq_33290233/article/details/117296946

**<font color='purple'>我们知道要分模块的话首先要用正确的语法把模块一个一个分出来，然后分出来以后模块中那些getters，mutations。。。方法的调用也要用新的语法进行重新调用对吧。</font>**

**示例：把user的相关数据都分出一个模块来**

- **<font color='blue'>1、在store模块下新建一个user.js，模块的语法如下（和vue2有一点点不同），最后export导出模块就行</font>**

- ```js
  import axios from 'axios';
  
  const user = {
      /** 1、这个箭头的写法就可以看出vuex3中模块划分的骚气之处了...*/
      state:() => ({
  
      }),
      getters:{
  
        },
        mutations:{
  
        },
        actions:{
          
        },
        modules:{
            
        }
  }
  
  export default user;

- **<font color='blue'>2、然后导入到store下的index.js中的moduels就行了</font>**
- ![image-20220318150146593](Typora_images/Vue4小时快速入门/image-20220318150146593.png)

- **<font color='purple'>3、调用vuex模块中的方法，可以和原来一样使用辅助函数直接调用，不过这样做的话会导致一个问题，那就是每一个模块中的函数命名不能有冲突，比如在user.js模块中我定义了totalPages方法，而在device.js模块中，我也同样定义了一个totalPages方法，这时候，控制台就会报错了，因为使用辅助函数的话是在vuex全局中调用指定的方法的，所以方法不能重名，不然就会出现命名冲突！</font>**



- **<font color='blue'>4、使用namespaced方法解决这个问题</font>**

- https://blog.csdn.net/qq_33290233/article/details/117296946

- ![image-20220318164933770](Typora_images/Vue4小时快速入门/image-20220318164933770.png)

- **5、每一个模块都用这条语句封装好，然后就剩下调用的语法了**

- 主要其实就两段代码：

  ```js
  import {  createNamespacedHelpers } from 'vuex' //引入辅助函数
  const { mapState, mapGetters, mapActions, mapMutations } = createNamespacedHelpers('模块名');
  ```

  

- ![image-20220318165405726](Typora_images/Vue4小时快速入门/image-20220318165405726.png)











## 9.5、vuex坑

### 9.5.1、vuex方法参数

**<font color='green'>//这里真是一个很大的坑我去！vuex中的所有方法，只能传一个外部的参数，如果有多个参数的话，就把它写成obj的形式！！！，不然这方法就根本执行不了！！！</font>**









# 10、vue过渡动画（学）

**==为什么需要vue动画呢？因为transition对于显示类的动画是实现不了的，所以vue专门开发了<transition>属性来实现一个框框从隐藏到显现的效果，当然它也可以用来实现其他的功能==**

## 10.1、\<transition>用法

```vue
<transition>
    <div v-show="isShow">
        <!--内容，各种dom...-->
    </div>
</transition>
```

1. **当isShow为真的时候div整个dom就会显示出来，要实现动画过渡的效果，就得先在外面套一层\<transition>**

2. **设置下面三个\<transition>专有类：**

.v-enter：当div刚进场时候的样式设置

.v-enter-active：div进场过程动画设置

.v-enter-to：div动画进场完毕后的样式设置

```css
.v-enter {
    opacity:0;  //设置div刚进场时不透明度为0
}
.v-enter-active {
    transition: all .3s ease-out;  //设置transition过渡
}
.v-enter-to {
    opacity:1;  //设置div进场完毕后完全显示
}
```

3. **当isShow为false的时候，div就会退场隐藏了，这时要实现动画过渡效果要设置下面三个专有类了**

.v-leave：当div刚离场时候的样式设置

.v-leave-active：div离场过程动画设置

.v-leave-to：div动画离场完毕后的样式设置

```css
.v-leave {
    opacity:1;  //离场开始时，为1
}
.v-enter-active {
    transition: all .3s ease-out;  //设置transition过渡
}
.v-enter-to {
    opacity:0;  //离场结束后，opacity为0
}
    
```

## 10.2、实现原理

基本原理还是transition的原理罢了。

**<font color='red'>在isShow变成真的那一刻，div的class中插入了.v-enter，变成了\<div class="v-enter">，然后这一瞬间div的样式中就了opacity:0; 然后迅速移除v-enter，将v-enter-active和v-enter-to移入div的class中，然后在.3s内就可以实现过渡效果了，当过渡结束后，一瞬间内移除v-enter-active和v-enter-to就行了；isShow变成false那一刻，过程也是一样的。</font>**

**<font color='blue'>如果div中有样式opacity:0.5;那么v-enter和v-enter-to中的opacity会在.3s覆盖掉原来的opacity的，然后等到动画结束后就能回复到opacity:0.5; 了</font>**

## 10.3、重命名

你可以为transition组件命名，比如\<transition name="list">，然后它的6个专有类就会变成这样了：

list-enter

list-enter-active

list-enter-to

list-leave

list-leave-active

list-leave-to



## 10.4、版本更新

**<font color='red'>vue3.x移除了v-enter和v-leave类，改为了v-enter-from和v-leave-from</font>**

## 10.5、注意事项

```vue
<transition>
    <div v-show="isShow">
        <!--内容，各种dom...-->
    </div>
    
    <div v-show="isShow">
        <!--内容，各种dom...-->
    </div>
</transition>
```

- ***<font color='red'>这种写法是错的！transition组件中只能有一个 dom 或 组件存在！！！</font>***

## 10.6、列表展开示例

  这是一个列表动画的演示

  完整代码：

  ```vue
  <template>
  
  <transition-group tag="ul" name="list"> <!--ul使用transition-group比较合理，当然transition也行-->
    <li class="item" @click="deleteItem"
        v-for="item in list"
        :key="item.id"
        style=""
    >
    {{item.title}}
    </li>
  <!--transition虚拟dom标签内部只能有一个 元素 或 组件-->
  <!--transition-group组件内部可以有多个元素 或 组件，但是的所有 元素或组件必须要有 :key!-->
  </transition-group>
    <br/>
    <button @click="addItem">增加一项</button>
  
  </template>
  
  <script>
  
  export default {
    data() {
      return {
        list:[
          {id:0,title:'默认向'},
        ]
      }
    },
    methods:{
      deleteItem() {
        this.list.pop();
      },
      addItem() {
        var id = this.list.length+1;
        this.list.push({id:id,title:'新增项'+id});
      }
    }
  }
  </script>
  
  
  <style>
  
  .item {
    width:200px;
    height: 40px;
    border: 1px solid #000;
  }
  /*进场过渡*/
  .list-enter-active,
  .list-leave-active {  /*离场过渡*/
    transition: all .3s linear;
  }
  
  .list-enter-from,
  .list-leave-to {
    height: 0px;
  }
  
  </style>
  ```

###   10.6.1、应用技巧（用）

**<font color='red'>1、把enter-from和leave-to和在一起，（enter-to和leave-from也是一样的）。</font>**

**<font color='red'>2、根据原样式，省略了enter-to和leave-from，减少了代码的冗余</font>**

***3、上面只是添加删除列表项的效果，对于展开列表项就有所不同了。***

****





# <font color='red'>0、vue设计的思路根源</font>

- 原来的前端页面是静态的，dom元素不能随着数据的更新而变化——》于是就有了vue的动态渲染dom（通过vue指令,data属性,methods属性实现）
- 原来前端页面有一大堆的dom结构，看着都烦——》于是就有了一个vue对象对应一整块的dom树（通过tmpelate模板，el挂载，虚拟dom实现）

- 想在一个文件中调用另一个文件中的对象、函数、常量——》于是就有了import... export...

- 现有html+css的页面设计，后有vue对代码结构进行优化！所以页面设计布局那些东西是大的，不能丢的！

# 1、整合Element UI

[Element-UI](https://github.com/ElemeFE/element)是`饿了么`前端团队推出的一款基于`Vue.js 2.0` 的桌面端UI[框架](https://so.csdn.net/so/search?q=框架&spm=1001.2101.3001.7020)，手机端有对应框架是 [Mint UI](https://github.com/ElemeFE/mint-ui) 。**<font color='pink'>简单来说就是vue解决了模块化，组件化开发的问题，可是页面的布局，设计还是得自己搞，于是就有了这玩意，帮助你在vue框架下，快速开发前端布局</font>**



## 10.1、下载element ui

在vue项目下

```bash
npm i element-ui -S  //安装element ui

npm install sass-loader@7.3.1 node-sass --save-dev  //安装sass加载器，注意版本兼容



```

## 10.2、导入Element UI

```javascript
//导入elementui
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
Vue.use(ElementUI);
```









# 1、springboot整合vue项目demo

参考：https://www.bilibili.com/video/BV14y4y1M7Nc/?spm_id_from=333.788.recommend_more_video.2



# 11.1、part1

**1、下载node版本为14.16.0，卸载原来的node环境，卸载方式：**

![image-20220228090859496](Typora_images/Vue4小时快速入门/image-20220228090859496.png)



下载地址：https://nodejs.org/download/release/v14.16.0/



node应用的目录结构：

![image-20220228092055489](Typora_images/Vue4小时快速入门/image-20220228092055489.png)

node_modules中就包含了在node环境下运行的应用程序项目，自带npm



**2、安装vue-cli**

```bash
npm install -g @v
```

**3、创建vue项目**

```bash
vue create springboot-vue-demo(这个是项目名)
```

![image-20220228094420451](Typora_images/Vue4小时快速入门/image-20220228094420451.png)



![image-20220228094548972](Typora_images/Vue4小时快速入门/image-20220228094548972.png)

敲空格就可以选中了。





![image-20220228094627364](Typora_images/Vue4小时快速入门/image-20220228094627364.png)

选择3.x版本的vue



![image-20220228094715578](Typora_images/Vue4小时快速入门/image-20220228094715578.png)

路由有两种：history模式和hash模式（根路径有#），选y



![image-20220228095315837](Typora_images/Vue4小时快速入门/image-20220228095315837.png)

**4、运行vue项目**

- 进入到项目springboot-vue-demo的路径下，运行npm run serve即可



**5、开发项目**

直接在idea中打开创建好的项目，进行代码的编辑，当然，在vscode中编辑也可以。

添加运行工具：

![image-20220228122047735](Typora_images/Vue4小时快速入门/image-20220228122047735.png)

==这些东西是什么？简单的说就是一个应用程序，这个程序可以让项目代码编译，并持久的运行起来。==



**6、使用到基于vue3.0的element plugin**

https://element-plus.gitee.io/zh-CN/guide/installation.html#%E4%BD%BF%E7%94%A8%E5%8C%85%E7%AE%A1%E7%90%86%E5%99%A8

- 参考上面的命令，在项目文件夹下下载plugin



- 然后引入pulgin对象
  - ![image-20220228135130252](Typora_images/Vue4小时快速入门/image-20220228135130252.png)



# 12、vue导入bootstrap4

```bash
cd front  //进入工程项目目录
npm install bootstrap@4.6.1 --save --save-exact  //保存到vue.package.json文件当中，并且指定精确的版本号
//bt4的依赖
npm install jquery@1.9.1 --save --save-exact
npm install popper.js@1.6.1 --save --save-exact

```



在main.js中全局导入bootstrap.min.css文件

```javascript
import 'bootstrap/dist/css/bootstrap.min.css'
```



# 13、vue前端加密

## 13.1、可逆/不可逆加密

### 13.1.1、md5不可逆加密

参考：https://www.bilibili.com/video/BV1H64y1U7pP?from=search&seid=4594769184219685649&spm_id_from=333.337.0.0

1、安装：

```bash
npm install js-md5
```

2、在组件中局部引入（vue2中可以全局注册该对象，vue3局部引入就行了）

```javascript
import md5 from 'js-md5'
```

3、在函数中调用就行了.

![image-20220313111331287](Typora_images/Vue4小时快速入门/image-20220313111331287.png)





### 13.1.2、AES可逆加密

![image-20220313112430125](Typora_images/Vue4小时快速入门/image-20220313112430125.png)

- 可逆的加密重要就是key秘钥了，加密端和解密端的key秘钥必须一致的，这样加密和解密两端才能成功。

- 

**==首先理解什么是crypto-js：`crypto-js` 是一个纯 `javascript` 写的加密算法类库 ，可以非常方便地在 `javascript` 进行 `MD5`、`SHA1`、`SHA2`、`SHA3`、`RIPEMD-160` 哈希散列，进行 `AES`、`DES`、`Rabbit`、`RC4`、`Triple DES` 加解密。==**

1、下载

```bash
npm install crypto-js --save-dev
```

2、写一个crypto.js文件，在里面引入crypto，然后编写加解密函数

这里采用的加密方式是AES；参考：https://blog.csdn.net/Umbrella_Um/article/details/99686988

```javascript
import CryptoJS from "crypto-js";

/**
 * 
 * CtyptoJS加密
 */
export function getAES(data){  //加密
    const key = CryptoJS.enc.Utf8.parse("1985718124500000");//加密秘钥
    const iv = CryptoJS.enc.Utf8.parse("1985718124500000");//偏移量
    let encrypted = '';  //加密后的接收变量
    const srcs = CryptoJS.enc.Utf8.parse(data);
    encrypted = CryptoJS.AES.encrypt(srcs,key,{
        iv:iv,
        mode:CryptoJS.mode.CBC,
        padding:CryptoJS.pad.Pkcs7
    });
    return encrypted.toString();
}



/**
 * CryptoJS解密
 */
export function getDAES(data){ //解密函数

    // console.log("参数传递:" + data);
    const key = CryptoJS.enc.Utf8.parse("1985718124500000");//加密秘钥
    const iv = CryptoJS.enc.Utf8.parse("1985718124500000");//偏移量

    var decrypted = CryptoJS.AES.decrypt(data,key,{
        iv:iv,
        mode:CryptoJS.mode.CBC,
        padding:CryptoJS.pad.Pkcs7
    });
    //  转换为 utf8字符串
    decrypted = CryptoJS.enc.Utf8.stringify(decrypted);
    return decrypted;
}
```

3、调用

在目标组件中引入导入这个文件曝露的两个函数接口，调用这两个函数就行了.

4、**<font color='purple'>老实说，这一串的代码都是没有什么意思的，都是调用crypt库，对数据进行加解密就行了，但是没有什么技术含量，只要会用就行了。不过倒是可以通过它的思路比较快速的去记忆它。</font>**

![image-20220313213800398](Typora_images/Vue4小时快速入门/image-20220313213800398.png)

- **==它的核心思路就是使用CryptoJS.AES.encrypt方式来进行明文的加密，然后传进一个明文，这个明文先做编码处理；然后再传入秘钥，秘钥的编码模式要和明文调整到一样，然后对加密进行配置，传进去一个对象，偏移量可以不设置，如果设置，那么其编码格式也要和明文&秘钥的编码格式相同，然后再传加密的模式，然后再传加密的填充。这个核心加密函数返回的是一个很复杂的对象，所以要把它转换为一个字符串形成最终的密文==**
- **==解密的核心函数就是CryptoJS.AES.decrypt，然后也是和加密函数一样的思路，最后转换成utf8编码的字符串还原数据就行了。==**



- 加密函数和解密函数加解密出来的对象都很奇怪》》》这个我还真的看不太懂。
  - ![image-20220313220208758](Typora_images/Vue4小时快速入门/image-20220313220208758.png)



## 13.2、实现密码传输加密

- 完全代码：

```java
https://blog.csdn.net/lizhenglyg/article/details/106193228
```









# 14、vue+springBoot+JWT登录验证

实现的功能逻辑：

![image-20220313151110474](Typora_images/Vue4小时快速入门/image-20220313151110474.png)

## 14.1、JWT介绍

https://www.bilibili.com/video/BV1cK4y197EM/?spm_id_from=333.788.recommend_more_video.-1

![image-20220313152009919](Typora_images/Vue4小时快速入门/image-20220313152009919.png)

JWT的组成：

![image-20220313152319007](Typora_images/Vue4小时快速入门/image-20220313152319007.png)

- 第一部分是header头的密文信息：
  - 头部明文：

![image-20220313152352773](Typora_images/Vue4小时快速入门/image-20220313152352773.png)

头部声明了令牌类型和加密的类型：就是alg变量。

- 第二部分是payload密文，就是存储有效信息的地方
  - 信息明文：

![image-20220313152637183](Typora_images/Vue4小时快速入门/image-20220313152637183.png)

- 第三部分是前两部分的密文拼接在一起的二次加密密文：

  - 算法：

  ![image-20220313152758211](Typora_images/Vue4小时快速入门/image-20220313152758211.png)

## 14.2、测试实现

- 先导入jar包：

```xml
        <!-- https://mvnrepository.com/artifact/io.jsonwebtoken/jjwt -->
        <dependency>
            <groupId>io.jsonwebtoken</groupId>
            <artifactId>jjwt</artifactId>
            <version>0.9.1</version>
        </dependency>
```

- jdk1.8以上的还要导入其他包，这里就不赘述了。





- 测试类：

  

 ```java
        private static final long day = 1000*60*60*24;
        private static final String key = "zzw@lty";
    
        /**
         * token生成
         */
        @Test
        public void Jwt(){
            //1、令牌生成器
            JwtBuilder jwtBuilder = Jwts.builder();
    
            String token = jwtBuilder
                    //header
                    .setHeaderParam("typ","JWT")
                    .setHeaderParam("alg","HS256")
                    //payload
                    .claim("name","root")
                    .claim("power",0)
                    //设置一下主题:就是为了区分识别用的
                    .setSubject("Jwt-Test")
                    //设置令牌有效时间
                    .setExpiration(new Date(System.currentTimeMillis() + day))
                    //设置令牌id
                    .setId(UUID.randomUUID().toString())
                    //Signature
                    .signWith(SignatureAlgorithm.HS256,key)
                    //最后拼接这三部分
                    .compact();
    
            System.out.println(token);  //测试输出token
    
    
        }
    
        /**
         * token解析
         */
        @Test
        public void parse(){
            String token = "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoicm9vdCIsInBvd2VyIjowLCJzdWIiOiJKd3QtVGVzdCIsImV4cCI6MTY0NzI0Njg3NCwianRpIjoiZjM1NDJkMmUtNmVkOS00NmE2LTk3NGEtMDJlM2Q4Y2JmZDM0In0.5y5V-20R3mIQtWvYByXcDyD5KPG8jcNZN-zMAvV-cLQ";
            /**
             * token解析器
             */
            JwtParser jwtParser = Jwts.parser();
            Jws<Claims> claimsJwt = jwtParser.setSigningKey(key).parseClaimsJws(token);
            Claims claims = claimsJwt.getBody();
            System.out.println(claims);  //2、这里就能拿到payload中的内容了捏。
    
        }
 ```

喷淋设备2





# 15、实时获取后端的数据

## 15.1、简介

- **<font color='red'>http请求只能由客户端去发起，所以几乎不能做到实时的数据查询，websocket协议就是解决这个问题的。</font>**



## 15.2、websocket的基本使用

```html
<input type="text" placeholder="请输入数据">
    <button>发送请求</button>
    <div>

    </div>
    <script>
        //websocket如何在浏览器端使用
        //H5中已经提供了websocket的API 可以直接使用
        var input = document.querySelector("input");
        var btn = document.querySelector('button');
        var div = document.querySelector('div');


        /** 1、创建一个socket对象*/
        /** 参数一：就是websokcet的服务地址*/
        var socket = new WebSocket('ws://echo.websocket.org');


        /** 2、当和接口服务器链接成功的时候就触发了这个事件*/
        socket.addEventListener('open',function() {
            console.log('监听事件已经开启');
            div.innerHTML = 'websocket接口链接成功了';
        });


        /** 3、主动给websocket接口发送消息*/
        btn.addEventListener('click',function(){
            var value = input.value;
            //向socket服务器发送数据
            socket.send(value);

        });

        /** 4、接受服务器端传回来的数据，数据以参数的形式放在回调函数的参数中*/
        socket.addEventListener('message',function(e){
            console.log(e.data);
        });
        
        /** 5、服务断开链接*/
        socket.addEventListener('close',function(){
            console.log('服务断开链接');
        });

    </script>
```



**<font color='purple'>主要就是new 一个webSocket对象，然后使用它的send方法和close方法，然后监听socket对象触发的事件->open事件，message事件，close事件还有一个error事件</font>**



## 15.3、使用nodeJS编写自己的websocket服务

tips:最好的cmd命令：https://www.cnblogs.com/huaxie/p/15438890.html

### part1、

创建一个工程目录，在目录下新建app.js文件，然后使用npm导入websocket依赖。

```bash
npm install nodejs-websocket
```



### part2、app.js

```js

/**1、导入这个包*/
const ws = require('nodejs-websocket');


/**2、创建一个server */
/**2.1、处理用户的请求 ：每次只要有用户链接,function函数就会被执行，会给当前链接的用户创建一个connetc对象*/
const server = ws.createServer(connect => {

    /**2.2、每当接受到用户传过来的数据，这个text事件就会被触发 */
    connect.on('text',data => {
        console.log('接受到了用户的数据' + data);
        /**2.3、给用户返回一些数据 */
        connect.send(data);

    });


    /**2.3、只要用户断开链接，close事件就会触发 */
    connect.on('close',() => {
        console.log('用户断开了');
    });


    /**2.4、错误处理：如果用户断开了和服务端的链接，那么他如果再发送数据的话会导致服务器报错然后整个停掉，这不好，所以要加上错误处理，保证服务端不停 */
    connect.on('error',() => {
        console.log('用户链接异常');
    });


});

/**3、监听一个端口，这里是3000，编写回调函数 */
server.listen('3000',() => {
    console.log('websocket服务启动成功了，监听了3000端口');

});





```

- **<font color='purple'>在终端使用node ./app.js就可以启动服务器了。</font>**

## 15.4、websocket

**<font color='purple'>本质很简单，就是前端一个socket对象，后端一个connect对象，一一对应，然后socket对象有监听事件，只要connect主动做一些事情，就能触发socket对象的监听事件的回调函数，同时socket对象还有send方法和close方法也可以触发connect对象的监听事件。相反的connect对象也是一样的，就是一个对象有监听事件的回调函数和触发事件的主动函数，然后两个对象交互数据而已捏。</font>**





# 16、后端实现刷脸登录

参考教程：https://www.bilibili.com/video/BV1mJ411k7nD?spm_id_from=333.999.0.0

## 16.1、百度云人脸识别的包

```xml
<!--        百度云API人脸识别的包-->
        <dependency>
            <groupId>com.baidu.aip</groupId>
            <artifactId>java-sdk</artifactId>
            <version>4.8.0</version>
        </dependency>
```



## 16.2、人脸识别接口调用方法

```java
/**
 * 人脸识别测试代码
 *
 * */
public class FaceTest {

    private AipFace client;

    public FaceTest(){
        //1、创建java代码和百度云交互的client对象
        //应用id，接口秘钥，应用秘钥，很safe对吧
        this.client = new AipFace("25939935","KGUsXe8bkZXea6ZYg78g7Hnd","d8nHXjW9WaGfosX5cjBS1IKrEgMC54IG");
    }

    @Test
    /**人脸注册接口测试
     * */
    public void testFaceRegister() throws IOException {
        //2、参数设置
        HashMap<String,String> map = new HashMap<>();
        map.put("quality_control","NORMAL");
        map.put("liveness_control","LOW");


        //3、构造图片
        String origin = "C:\\Users\\Lenovo\\Pictures\\人脸识别\\魏梦莺1.jpg";
        //上传图片到百度的人脸识别库有两种方式：1、url 2、base64加密传输
        //根据路径直接获取到文件的字节数组
        byte bytes[] = Files.readAllBytes(Paths.get(origin));
        //使用百度的工具类进行base64字符串加密转换
        String base64 = Base64Util.encode(bytes);

        //4、调用API方法完成人脸注册
        /**
         * 参数一：图片的url或者base64字符串
         * 参数二：图片的形式：url或者base64
         * 参数三：组id，就是百度应用里面的组id（固定字符串就行）
         * 参数四：用户id，就是百度应用里面的用户id
         * 参数五：map参数
         * */
        JSONObject object = client.addUser(base64,"BASE64","itcast","1002",map);
        System.out.println(object.toString(2));

    }



    /**
     * 有时候上传到百度人脸库里面的照片中没有人脸，那就很不行了。所以要有这个检测的功能
     * 人脸检测
     *
     * */
    @Test
    public void testIsFaceImg() throws IOException {
        //构造图片
        String origin = "C:\\Users\\Lenovo\\Pictures\\Saved Pictures\\good.jpg";
        //上传图片到百度的人脸识别库有两种方式：1、url 2、base64加密传输
        //根据路径直接获取到文件的字节数组
        byte bytes[] = Files.readAllBytes(Paths.get(origin));
        //使用百度的工具类进行base64字符串加密转换
        String imgBase64 = Base64Util.encode(bytes);


        //2、调用client的检测方法进行检测
        JSONObject object = client.detect(imgBase64,"BASE64",null);
        System.out.println(object.toString(2));

    }

    /**
     * 人脸比对接口，就是把指定的图片和你的应用数据库中的所有图片进行比对，并返回相似度最高的几个用户的list
     * 一般来说list当中score评分字段值>80才可以认定为同一个人。低于80分的都不是同一个人！！！要注意
     * */
    @Test
    public void testFaceSearch() throws IOException {
        //构造图片
        String origin = "C:\\Users\\Lenovo\\Pictures\\人脸识别\\魏梦莺1.jpg";
        //上传图片到百度的人脸识别库有两种方式：1、url 2、base64加密传输
        //根据路径直接获取到文件的字节数组
        byte bytes[] = Files.readAllBytes(Paths.get(origin));
        //使用百度的工具类进行base64字符串加密转换
        String imgBase64 = Base64Util.encode(bytes);


        //2、调用search方法进行查询
        JSONObject object = client.search(imgBase64,"BASE64","itcast",null);
        System.out.println(object.toString(2));



    }


    /**
     * 人脸库更新的操作
     *因为人的相貌会变的，所以还是得有人脸更新的功能
     *和注册的唯一不同就是 函数名不同，接口不同（updateUser），图片和原来不一样了，其他都是一样的
     * */
    @Test
    public void testFaceUpdate() throws IOException {
        //2、参数设置
        HashMap<String,String> map = new HashMap<>();
        map.put("quality_control","NORMAL");
        map.put("liveness_control","LOW");

        //3、构造图片
        String origin = "C:\\Users\\Lenovo\\Pictures\\人脸识别\\吴梦圆2.jpg";
        //上传图片到百度的人脸识别库有两种方式：1、url 2、base64加密传输
        //根据路径直接获取到文件的字节数组
        byte bytes[] = Files.readAllBytes(Paths.get(origin));
        //使用百度的工具类进行base64字符串加密转换
        String base64 = Base64Util.encode(bytes);

        //4、调用API方法完成人脸注册
        /**
         * 参数一：图片的url或者base64字符串
         * 参数二：图片的形式：url或者base64
         * 参数三：组id，就是百度应用里面的组id（固定字符串就行）
         * 参数四：用户id，就是百度应用里面的用户id
         * 参数五：map参数
         * */
        JSONObject object = client.updateUser(base64,"BASE64","itcast","1001",map);
        System.out.println(object.toString(2));

    }





}
```



## 16.3、google提供的二维码生成包

```xml
<!--        google提供的二维码生成的包-->
        <dependency>
            <groupId>com.google.zxing</groupId>
            <artifactId>core</artifactId>
            <version>3.2.1</version>
        </dependency>

        <dependency>
            <groupId>com.google.zxing</groupId>
            <artifactId>javase</artifactId>
            <version>3.2.1</version>
        </dependency>

```



### 16.3.1、生成二维码的方式

```java
//生成二维码的测试
public class QRCodeTest {
    /**
     * 生成本地二维码的教程
     * **/
    public void generatorQRCodeLocal() throws Exception {
        //1、设置要存储到二维码中的信息
        String content = "https://www.bilibili.com/";

        //2、通过zxing包生成二维码图片（可以保存二维码到本地，也可以通过data url的方式来访问）
        //创建QRWriterCode对象
        QRCodeWriter writer = new QRCodeWriter();
        //传参生成二维码
        BitMatrix bt = writer.encode(content, BarcodeFormat.QR_CODE,200,200);

        //3、保存生成的二维码到本地
        Path path = new File("C:\\Users\\Lenovo\\Pictures\\人脸识别\\test.png").toPath();
        MatrixToImageWriter.writeToPath(bt,"png",path);

    }



    public static void main(String[] args) throws Exception {

        /**
         *
         *生成二维码url的方法
         * */
        String content = "https://www.bilibili.com/";
        QRCodeWriter writer = new QRCodeWriter();
        BitMatrix bt = writer.encode(content, BarcodeFormat.QR_CODE,200,200);

        //1、拿到流信息进行base64的编码处理就行了
        //将二维码bt以字节数组的形式保存到输出流当中去
        ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
        BufferedImage image = MatrixToImageWriter.toBufferedImage(bt);
        ImageIO.write(image,"png",outputStream);  //这一步完成后outputStream对象中就有了二维码的字节流了

        //2、对字节流进行base64的处理
        String encode = Base64Util.encode(outputStream.toByteArray());

        //3、生成url base64访问
        String url = new String("data:image/png;base64," + encode);

        System.out.println(url);

    }

}

```





































# 99疑问：

1、为什么在img附近的标签中使用了{{}}语法后，img自身的宽和高就变成0了？？？

2、为什么在beforeRouteEnterF钩子函数中无法获取到sessionStorage中的值？？？不过在created钩子函数中是可以的???

3、大小写要注意：比如一个组件叫Aside，那么调用它时应该是 \<Aside>\</Aside>，如果字母小写就不起作用了

如果一个组件叫AsideNav那么调用它时只能用 \<aside-nav>\</aside-nav>

4、height: calc(100vh - 60px);  如果运算符中间没有空格的话会报错的！！！

5、默认布局流中伸缩效果的实现，只要调整margin-left不就行了吗，我透了服了...

6、得想办法让vue中调用的函数都接口话，不然的话一条一条语句改的话，真的很麻烦！



显示过渡 和 进出场过渡动画效果：



# 20、综合应用技巧

<div style="background-color:black;color:white;border:1px solid white;font-size:18px;">技巧一：标志位改变函数</div>

**<font color='#007BFF'>	我们通常通过标志位来改变一个元素的样式，所以经常会写一个函数然后改变组件的标志位变量来让样式发生变化，可是实际情况中，往往是标志位改变后还要做一大堆的其他处理，所以我们就把if...else...这段代码加到标志位改变函数中，让它的接口复用性更加强大</font>**

```javascript
ChangeFlag(){
    this.flag = !this.flag;
    if(this.flag == true){
        //do something
    }else {
        //do other things
    }
}

```



# 21、准备

## 1、computer属性的get和set方法

- 计算属性可以进行get和set

![image-20220514135440895](Typora_images/Vue4小时快速入门/image-20220514135440895.png)

## 2、watch监听对象

- 监听对象的方法

  ![image-20220514135627813](Typora_images/Vue4小时快速入门/image-20220514135627813.png)



## 3、v-if和v-for不连用

- ![image-20220514140633272](Typora_images/Vue4小时快速入门/image-20220514140633272.png)

- **<font color='purple'>如果按照框框里这样写的话，会先遍历出一项，然后在判断v-if中的这一项该不该存在，但这样太耗费资源了，一般来说要么直接不渲染这整个的列表然后再外面加一个v-if就行了；要么直接在每一项的内部再加一个v-if判断这一项该不该出现，就这样哈哈</font>**



## 4、获取事件对象

![image-20220514141443726](Typora_images/Vue4小时快速入门/image-20220514141443726.png)



## 5、父子组件传递参数

props和$emit事件

## 6、兄弟组件传递参数

先定义一个新的vue对象在js文件里

![image-20220514142753098](Typora_images/Vue4小时快速入门/image-20220514142753098.png)



- **传递参数方：**
  - ![image-20220514143029119](Typora_images/Vue4小时快速入门/image-20220514143029119.png)
- **接受参数方：**
  - ![image-20220514143308803](Typora_images/Vue4小时快速入门/image-20220514143308803.png)

- **避免内存泄漏：**
  - ![image-20220514143403625](Typora_images/Vue4小时快速入门/image-20220514143403625.png)



## 7、父子组件的创建挂载顺序

- ![image-20220514143724664](Typora_images/Vue4小时快速入门/image-20220514143724664.png)



## 8、nextTick

![image-20220514144618026](Typora_images/Vue4小时快速入门/image-20220514144618026.png)

- **<font color='purple'>就是当数据改变的时候vue会重新渲染对应的dom对吧，但是呢，如果你再一改变数据的时候就去访问那个dom元素你会发现，你获取到的还是原来的那个dom。因为vue是异步渲染dom的所以，当你改变数据的时候他会在下一个Tick中重新渲染dom，这时候你如果想要获取到最新的dom就可以用上面的nextTick API了。</font>**



## 9、作用域插槽



![image-20220514150152612](Typora_images/Vue4小时快速入门/image-20220514150152612.png)



- 在父组件中使用该组件的时候，如果开始标签和结束标签中没有内容，那么就会默认显示 ’“哈默”，如果有内容，那么原来的“哈默”就会被覆盖掉了，如果想在父组件中使用该组件然后还显示该组件内部的数据怎么办呢？



![image-20220514150551339](Typora_images/Vue4小时快速入门/image-20220514150551339.png)

- **<font color='purple'>这样做的话相当于，该子组件把自己的user对象传递给了 slot的user属性了。</font>**

![image-20220514150834860](Typora_images/Vue4小时快速入门/image-20220514150834860.png)

- **<font color='purple'>然后在父组件中使用该组件的时候，在内容中写入\<template>通过v-slot属性获得插槽中的user属性的值，然后就可以使用差值表达式了。这里的default是表示默认的那个插槽，你还可以给插槽取个名字的。</font>**



## 10、动态组件

![image-20220514172502283](Typora_images/Vue4小时快速入门/image-20220514172502283.png)

- **<font color='red'>所谓的动态组件就是根据数据的不同来指定使用不同的组件，一般来说是比较有用呢的。</font>**

## 11、异步加载组件

**<font color='red'>异步组件就是说在渲染一个vue页面的时候没有必要把所有的内容都一次性进行加载到app.js文件中，等到axios访问或者vi-if为true显示的时候再载入，这样可以大大提高页面加载的效率，给用户端良好的体验！</font>**

实现

![image-20220514173843158](Typora_images/Vue4小时快速入门/image-20220514173843158.png)



## 12、组件缓存

**<font color='purple'>像我之前做项目的时候就遇到过这样的问题就是，要通过一个data值的改变来切换当前页面的组件，这就会造成组件的渲染和销毁，从而导致项目性能的下滑，非常不好！，所以可以使用keep-alive切换组件的时候进行缓存就行了。</font>**

![image-20220514174240800](Typora_images/Vue4小时快速入门/image-20220514174240800.png)





## 13、抽离组件公共数据和方法

- 定义一个mixin文件：

![image-20220514175659987](Typora_images/Vue4小时快速入门/image-20220514175659987.png)



- 导入mixin：



![image-20220514175800882](Typora_images/Vue4小时快速入门/image-20220514175800882.png)



## 14、setup函数

![image-20220514180440220](Typora_images/Vue4小时快速入门/image-20220514180440220.png)

## 15、vue3和vue2的本质区别

很好的教程：https://www.bilibili.com/video/BV1yp4y1S775?from=search&seid=18172997045779936522&spm_id_from=333.337.0.0

- 最主要的就是设计思路的不同
  - 在vue2中使用的options API的设计思路
  - 而在vue3中使用的是composition API的设计思路



- vue2有一个很大的问题就是在一个组件中如果有很多的函数的话，就很难管理区分。。。。

- vue3允许你能把函数和数据提取出来单独封装起来提高了开发效率：

![image-20220517073159776](Typora_images/Vue4小时快速入门/image-20220517073159776.png)



![image-20220517073403936](Typora_images/Vue4小时快速入门/image-20220517073403936.png)





- 这样看上去还是有点烂，所以再提取优化一下：

- 抽离函数：

![image-20220517073638178](Typora_images/Vue4小时快速入门/image-20220517073638178.png)

- 解构函数

![image-20220517074147437](Typora_images/Vue4小时快速入门/image-20220517074147437.png)



## 16、环境变量















# 22、基础知识巩固

## 22.1、js日期操作

https://www.bilibili.com/video/BV1of4y1S7cn?from=search&seid=17203817589969638857&spm_id_from=333.337.0.0

- **日期的操作归纳起来无非两点：第一先获取日期对象，第二在再调用对象的方法而已。**



### 日期对象的创建：

![image-20220605135324924](Typora_images/Vue4小时快速入门/image-20220605135324924.png)

- **<font color='red'>当在控制台上打印的时候，打印的是toString()方法后的字符串。</font>**



### **<font color='red'>常用的方法：</font>**

![image-20220605140618463](Typora_images/Vue4小时快速入门/image-20220605140618463.png)



### 常用操作

- **日期对象的格式化**

```js
/**
 * 函数作用：把一个日期对象转换成日期字符串
 * @param {Date} date 
 * @returns 
 */
export const date2Str = date => {
  let year = date.getFullYear();
  let month = date.getMonth() + 1;
  let day = date.getDate();
  let dateStr = `${year}-${month < 10 ? '0' + month : month}-${day < 10 ? '0' + day : day}`;
  return dateStr;
}
```

- **获取今天是礼拜几**

```js
 export const getWeekDate = () => {
      let now = new Date();
      let day = now.getDay();
      let weeks = new Array(
        "周日",
        "周一",
        "周二",
        "周三",
        "周四",
        "周五",
        "周六"
      );
      let week = weeks[day];
      return week;
}
```

## 22.2、js数组操作

- **数组方法无非看三点：1干了什么了、2返回值是什么、3是否改变原arr**

### 1、数组转字符串

- **toString() 方法**

- **join(split?: string) 方法，这个方法相当于str.split()，可以指定字符串的分割符**

  ```js
  let arr = [1, 3, 5, 7, 9];
  let str = arr.join('/');
  /**返回一个str，不改变原arr */
  ```

  

### 2、堆栈方法

- **push() 方法：<font color='red'>向数组末尾添加一个或多个元素，返回值是添加后的数组的长度，改变原arr</font>**

- **pop()方法：弹出数组最后一个元素，返回值是被弹出的那个元素，改变原arr**
- 下面两个是对第一个元素的出入栈操作，和push/pop没什么不同

![image-20220605150909867](Typora_images/Vue4小时快速入门/image-20220605150909867.png)



### 3、排序方法

- **reverse()方法：将数组倒序排序，并返回倒排后的数组，改变原arr**
- **sort()方法：正向排序，其他同上**

- 实现乱序的方法：
  - ![image-20220605151627159](Typora_images/Vue4小时快速入门/image-20220605151627159.png)

### 4、数组拼接

- **concat()方法，实现数组拼接，返回拼接后的arr数组，不改变原arr!**

```js
let arr = [1, 3, 5, 7, 9];
// console.log(arr.concat(3,4));
// console.log(arr.concat([3,4]));
console.log(arr.concat([1,2,[3,[1,1,11]]]));
```

- **es6语法，使用...运算符**

```js
console.log([...arr,78,98]);
```

- **<font color='red'>深拷贝和浅拷贝的区别，一个是拷贝对象的内容，指针是新的指针；一个是拷贝一份指针，两个指针变量都指向同一块内存！</font>**



### 5、数组删改

- **<font color='red'>slice()方法：参数一：截取的起始下标，参数二：截取的结束下标【可以不填】；左闭右开；返回一个新的arr，不改变原arr</font>**

  - 高级操作：把类数组，转成数组：

  - ```js
    let str  = '123456';
    console.log(Array.prototype.slice.call(str));
    //为什么要这样调用slice方法呢？因为正常调用都是 arr.slice()这样的，但是现在没有arr了所以用原型的方法。
    //不改变原str
    ```
    
  - 输出：[ '1', '2', '3', '4', '5', '6' ]
  
  - ***<font color='#39e600'>小结：slice返回一个的新的截取下来的arr;</font>***



- **<font color='purple'>splice()方法：截取数组或添加新元素到数组中，改变原arr</font>**

  - **如果什么都不传：**

  ```js
  let arr = [1, 3, 5, 7, 9];
  
  console.log(arr,arr.splice());
  ```

  - 输出：[ 1, 3, 5, 7, 9 ] []
  - **传一个参数4：**

  ```js
  let arr = [1, 3, 5, 7, 9];
  
  console.log(arr,arr.splice(4));
  ```

  - 输出：[ 1, 3, 5, 7 ] [ 9 ]
  - **<font color='blue'>说明，splice改变原arr，返回的是截取下来的那一段数组，然后当只传一个参数的时候也是 左闭右开和slice一样的。</font>**
  - **传两个参数，参数一代表截取的起始index，参数二代表截取长度；**
  - ***<font color='#39e600'>小结：splice不仅会返回一个新的截取下来的arr，也会真的改变原arr的</font>***
  - ***<font color='red'>传递三个以及以上的参数，第一个就是数组插入的起始位置，第二个参数写0表示截取长度为0，第三个参数就是要插入的数据了【不常用】</font>***
  - **小结：为什么splice会这么复杂，因为它本来想要替换数组中的某一段，然后把被替换的部分保存下来而已**

### 6、返回数组下标

- indexOf()，搜索指定元素在数组中的下标
- lastIndexOf()，从右往左查找，返回值和上述的是一样的。
- ES6：find方法和findIndex()方法；

 ![image-20220605175652297](Typora_images/Vue4小时快速入门/image-20220605175652297.png)





### 7、ES6新方法

- 都是静态方法：

- **Array.of()方法：创建一个新的数组**

  - ```js
    const arr = Array.of(3);
    console.log(arr);
    
    const arr1 = Array.of(4,5,6);
    console.log(arr1);
    ```

  - 输出：

  - ![image-20220605171307484](Typora_images/Vue4小时快速入门/image-20220605171307484.png)

  - **<font color='purple'>为什么要搞这样一个方法呢？因为如果使用new Array(3)；会创建一个3个长度的空的数组，但是使用new Array(3,4,5)；就会创建一个[3,4,5]这样的数组，这会引起歧义，所以使用of方法创建具体数组就行了！</font>**

- **Array.from()方法：和slice()的高级用法是一样的，把类数组转换成数组**

  - ```js
    Array.from('142563')
    ```

  - 输出：[ '1', '4', '2', '5', '6', '3' ]



### 8、接收任意多个参数的函数写法

![image-20220605172439132](Typora_images/Vue4小时快速入门/image-20220605172439132.png)



### 9、数组遍历

#### 9.1、遍历对象所有属性的方法

```js
const obj = {
    c: 'hyf',
    a: 'zzw',
    b: 'xj',
    d: 'lyh'
};
//遍历所有的键
for(let value of Object.keys(obj)) {
    console.log(value);
}
//遍历所有的值
for(let value of Object.values(obj)) {
    console.log(value);
}
//遍历所有的键值对，然后通过解构的方式来赋值
for(let [key,value] of Object.entries(obj)) {
    console.log(key,value);
}
```

- **<font color='red'>在ES6中的数组的原型对象上也有这样对应的三个方法，不过keys对应的是数组的下标而已。</font>**

```js
const arr = ['zzw','lty','xj','hyf','lyh'];

for(let value of arr.keys(obj)) {
    console.log(value);
}

for(let value of arr.values(obj)) {
    console.log(value);
}

for(let [key,value] of arr.entries(obj)) {
    console.log(key,value);
}
```

#### 9.2、数组遍历的所有方法

**<font color='purple'>map、forEach、filter、some、every</font>**

![image-20220605190651998](Typora_images/Vue4小时快速入门/image-20220605190651998.png)

- 上面的所有的方法的第一个参数都是这样的一个function函数；

**/+++++++++++++++++++++++++++++++++++forEach()使用++++++++++++++++++++++++++++++++++++++++++++++++++/**

- **forEach()讲解**

  - ```js
    let arr = [1,2,3,5,3,2];
    arr.forEach((item,index,arr) => {
        console.log(item,index,arr);
    });
    
    ```

  - 输出：

  - 1 0 [ 1, 2, 3, 5, 3, 2 ]
    2 1 [ 1, 2, 3, 5, 3, 2 ]
    3 2 [ 1, 2, 3, 5, 3, 2 ]
    5 3 [ 1, 2, 3, 5, 3, 2 ]
    3 4 [ 1, 2, 3, 5, 3, 2 ]
    2 5 [ 1, 2, 3, 5, 3, 2 ]

  - **forEach()是没有返回值的，就算你指定返回值给它，它也没有返回值的。**

    ```js
    let arr = [1,2,3,5,3,2];
    console.log(arr.forEach((item,index,arr) => {
        return 1;
    }));
    ```

    ![image-20220605191655858](Typora_images/Vue4小时快速入门/image-20220605191655858.png)

  

  - **<font color='red'>forEach()中的第二个参数，用于指定回调函数的this指针；</font>**

  - ```js
    let arr = [1,2,3,5,3,2];
    
    let obj = {
        name: 'zzw',
        arg: 18
    }
    
    arr.forEach(function(item,index,arr) {
        console.log(this);
    },obj);
    ```

  - **这时候打印出来的就是obj对象了，如果obj不指定，this就不知道是什么东西了，如果是在.html页面写的脚本，this默认就是windows了，这个参数可以省略 let _this = this;的这种写法了。**

  - ![image-20220605193801704](Typora_images/Vue4小时快速入门/image-20220605193801704.png)
  - **<font color='purple'>第一种写法，指定了第二个参数是obj的this指针，所以console出来的也是obj对象；而使用箭头函数直接就可以打印出来了，因为箭头函数没有自己的构造方法，所以，在它里面使用this一定是父对象的this指针。</font>**
  - **forEach()遍历稀疏数组**
  - **<font color='purple'>稀疏数组就是 let arr = [1, ,3, ,4, 5]这样类似的数组，也可以通过delete arr[index]的方式创建稀疏数组，在使用forEach进行遍历的时候，不会遍历到空的值，所以上述数组只会循环4次，和for i不太一样。</font>**
  - **<font color='red'>forEach()不支持break;和continue语句，对循环的操控性是很有限的。</font>**
  - **任意多个参数的使用二**

  ![image-20220605195633151](Typora_images/Vue4小时快速入门/image-20220605195633151.png)



**/+++++++++++++++++++++++++++++++++++map()基础使用++++++++++++++++++++++++++++++++++++++++++++++++++/**

- **<font color='purple'>map()和forEach()一样都可以用来遍历数组，不过map方法是有返回值的，返回值是一个对于原数组的映射，就比如我有一个[1,2,3]这样的数组，我想把它的每一项都*2，得到[2,4,6]这样的一个数组，这时候我们就可以使用map方法了。</font>**

- ```js
  let arr = [1,2,3];
  
  let arr1 = arr.map((item,index,arr) => {
      return item*2;
  });
  
  console.log(arr,arr1);
  ```

- ***<font color='#39e600'>小结：map函数中的回调函数的返回值就是新的映射数组中的每一项的值了。不改变原arr</font>***

**/+++++++++++++++++++++++++++++++++++filter()基础使用++++++++++++++++++++++++++++++++++++++++++++++++++/**

- **<font color='purple'>filter()就是为了过滤数组用的，其回调函数的返回值必须是一个bool值，用以决定这一项要不要在新的arr中被过滤掉</font>**

```js
let arr = [1,2,3];
let arr1 = arr.filter((item,index,arr) => {
    return item === 2? false: true;  //像这样的三元表达式的用法太捞了，直接用item !== 2;不就好了吗
});

console.log(arr1);
```

- **把元素值为2的那一项过滤掉。**

- 常见需求，过滤掉一个数组中的undefined和null：

![image-20220605204156038](Typora_images/Vue4小时快速入门/image-20220605204156038.png)



**<font color='red'>null和undefined的区别：null代表的是一个空指针，而undefined代表的是一个空的值，正因为如此所以null == undefined是成立的，但是 null === undefined就不成了，因为这里取消了隐式转换。</font>**



**/++++++++++++++++++++++++++++++some()/every()基础使用++++++++++++++++++++++++++++++++++++++++++++++++++/**

![image-20220605205628923](Typora_images/Vue4小时快速入门/image-20220605205628923.png)

- **返回值res1为true，res2为false，这两个主要是用来检测数组是否符合莫一种给定的标准的。**



#### 9.3、reduce方法

- **<font color='purple'>也叫做累加归并方法，这个方法就能实现很多的骚操作了。</font>**

```js
let arr = [1,2,3,4,5];
let res = arr.reduce((accumulation,item,index,arr) => {
    return accumulation + item;
});
console.log(res);
```

- **<font color='red'>和其他方法不同的是，回调函数中多了一个累加器，accumulation，累加器的初始值可以通过第二个参数指定，默认是数组的第一个值；进入第一轮循环，因为1被accumulationi取走了所以 item从2开始，1+2=3，所以下一次循环开始时，accumulation的值就是3了，就是这样一只值累加，最终返回15；</font>**

- **也可以指定初始值，这样循环就会从第一位开始了**

```js
let arr = [1,2,3,4,5];
let res = arr.reduce((accumulation,item,index,arr) => {
    return accumulation + item;
},90);
console.log(res);
```

这样就是105了。

- **常用需求，将二维数组转化为一维数组：**

- ```js
  let arr = [[1,2],[3,4],[5,6]];
  let res = arr.reduce((accumulation,item) => {
      return accumulation.concat(item);
      // return [...accumulation,...item]
  },[]);
  console.log(res);
  ```

- 

## 22.3、this指向的四种绑定规则

教程：https://www.bilibili.com/video/BV1NT4y1j7xH?p=1

### 1、默认绑定：默认绑定窗口window对象

- 在在html的\<script>标签中，this默认指向window对象

```js
console.log(this === window);  //打印的结果是true
```

- 在.js文件中 默认指向一个空的对象

```js
console.log(this);  //打印结果是一个空对象
```

### 2、隐式绑定：谁调用就绑定谁

```js
let obj = {
    a: 2,
    foo: function() {
        console.log(this);
    }
};

obj.foo();
```

打印：
![image-20220607070331260](Typora_images/Vue4小时快速入门/image-20220607070331260.png)

- **<font color='purple'>每一个普通函数都有自己的this指针变量，不过具体指向谁，就要看情况了。</font>**



- **<font color='red'>又可以在函数内部，定义一个新的函数，并且执行它</font>**

![image-20220607071342681](Typora_images/Vue4小时快速入门/image-20220607071342681.png)

**<font color='blue'>在html\<script>中，第一个this指向的是obj对象，第二个this指向的是window对象；而在.js文件中，第二个对象指向的是一个全局的Object对象：</font>**

![image-20220607072206962](Typora_images/Vue4小时快速入门/image-20220607072206962.png)

- **<font color='blue'>在上面这种情况中，test函数一被定义完就立即调用了，称作立即调用函数，立即调用函数可以用下面的这种写法：</font>**

```js
(function(){
    ...
})();  //这样定义的函数就会被立即调用了。
```



**<font color='green'>闭包简单了解：</font>**

![image-20220607075445231](Typora_images/Vue4小时快速入门/image-20220607075445231.png)

- **<font color='red'>就是当函数执行的时候，定义了一个新的函数并且return这个函数指针就叫闭包；</font>**

**<font color='purple'>当闭包函数执行的时候里面的绑定指向谁呢：还是window或者是全局的Object对象，因为this这个指针指向的一定是一个对象，所以不必考虑this指向一个函数指针，因为没有意义，你指向一个函数不如直接调用它就行了。。。</font>**

```js
let obj = {
    a: 2,
    foo: function() {
        //闭包
        function test() {
            console.log(this);
        }
        return test;
    }
};
//执行闭包函数
obj.foo()();

```

特殊案例：

```js
//全局函数
function foo() {
    console.log(this);
}

let obj = {
    a: 2,
    foo: foo
}

let ptrFn = obj.foo;

ptrFn();

```

**this也是windows或者是全局的obj，道理很简单，因为这样做就相当于直接在全局使用 foo(); 而已嘛**



当把函数作为参数传递给另一个函数调用，那个它的this肯定还是全局的obj或者是window对象，因为this不可能指向一个函数嘛。。。

```js
//全局函数
function foo() {
    console.log(this);
}

//把函数作为参数进行传递
function test(fn) {
    fn();
}

let obj = {
    a: 2,
    foo: foo
}

test(obj.foo);
```

==注意：形参被赋值为实参的时候，是浅拷贝！==

不过fn()的this指向是可以被父函数改变的，就是使用fn.call(obj); 函数fn的this指向就可以被改变了,就会指向obj

***<font color='blue'>小结：父函数有能力决定子函数的this指向</font>***

***<font color='#39e600'>小结1：隐式绑定有时候会出现 隐式丢失，以及父函数决定子函数this指向的情况</font>***

### 3、显示绑定：call，apply，bind

![image-20220608165037061](Typora_images/Vue4小时快速入门/image-20220608165037061.png)

### 4、new一个函数

```js
function Person() {
    console.log(this);
}
let person = new Person();
```

- 这个this就会指向 一个Person {}对象：

![image-20220608170121493](Typora_images/Vue4小时快速入门/image-20220608170121493.png)

**<font color='green'>道理很简单，因为当你new 一个函数的时候，就相当于把Person函数当做了一个类构造函数，构造函数指向的this当然是类的一个具体的对象啦，并且还会返回【默认返回】给person变量。</font>**



**小结：函数this绑定的优先级：new > call、apply、bind > 隐式 >默认**



## 22.4、箭头函数的this

- 箭头函数为什么会产生呢？就是当子函数想要使用父函数的this指针的时候，要用到如下操作：

```js
function foo() {
    //先把父函数的this指向保存下来，然后在在子函数中进行调用
    let _this = this;
    function test() {
        console.log(_this);
    }
    test();
}

let obj = {
    a: 2,
    foo: foo
}
obj.foo();
```

当然除了这种方式以外还有另一种方式：

```js
function foo() {
    function test() {
        console.log(this);
    }
    //使用显示绑定强行绑定父函数指向的this
    test.call(this);
}

let obj = {
    a: 2,
    foo: foo
}
obj.foo();
```

<font color='green'>**当然这些方式都显得十分的繁琐，所以箭头函数就出来了，箭头函数绑定<font color='red'>父级作用域</font>的this指针，也就是说箭头函数的this只由父级作用域的this指向决定。**</font>



案例：

```js
let obj = {
    a: 2,
    foo: () => {
        console.log(this);
    }
}

obj.foo();
```

**<font color='blue'>这个打印的结果是什么呢？因为箭头函数没有自己的this的，写在它里面的this是父级作用域的this,所以是全局obj或者是window。。。</font>**

什么隐式绑定，显示绑定，都对箭头函数无效的，new tm的更加了，箭头函数连自己的this都没有，还new个毛线！







# 23、video标签



https://www.bilibili.com/video/BV1iF411x7kw?spm_id_from=333.999.0.0&vd_source=365d13057e58bb6a007cdd5275785229

![image-20220620065201783](Typora_images/Vue4小时快速入门/image-20220620065201783.png)

- src：视频的源地址
- controls：就可以为视频添加默认的一些控件了。
- autoplay：设置了该标签后video就会自动播放。（单独设置autoplay是不会播放的，还要设置muted静音属性，这主要是为用户体验考虑的）
- muted：该属性使得视频静音。
- loop：循环播放。
- poster：设置视频播放前显示的图像。

![image-20220620070024541](Typora_images/Vue4小时快速入门/image-20220620070024541.png)





![image-20220620070900498](Typora_images/Vue4小时快速入门/image-20220620070900498.png)

![image-20220620072253835](Typora_images/Vue4小时快速入门/image-20220620072253835.png)





# 24、仿站小工具

- 有时会遇到经常要我们前端模仿一个页面的业务情况产生，这个时候就要使用到仿站小工具了。
- 仿站工具：https://www.toolnb.com/tools/fangzhan.html

参考：https://www.jianshu.com/p/706f30fb65c3



# 25、开发环境配置

https://www.bilibili.com/video/BV1594y1f78z?from=search&seid=16418438584818318283&spm_id_from=333.337.0.0&vd_source=365d13057e58bb6a007cdd5275785229



百度资料：

https://blog.csdn.net/muzidigbig/article/details/115665717

```js
module.exports = {
  // 部署打包时候的路径
  publicPath: process.env.NODE_ENV === 'production' ? './' : '/',
  // npm run build时候的输出路径
  outputDir: 'dist',
  lintOnSave: process.env.NODE_ENV === 'development',
  productionSourceMap: false,
  // 开发环境配置
  devServer: {
    host: '0.0.0.0',
    port: 3000,
    open: true,
    // 服务器环境配置
    proxy: {
      // detail: https://cli.vuejs.org/config/#devserver-proxy
      [process.env.VUE_APP_BASE_API]: {
        // 如果是配置代理的话，那么这个也要改变的
        target: 'http://localhost:8188',
        changeOrigin: true,
        pathRewrite: {
          ['^' + process.env.VUE_APP_BASE_API]: ''
        }
      }
    },
    disableHostCheck: true
  }
}

```

==服务器配置，就是用来解决跨域的问题的，会把process.env.VUE_APP_BASE_API这里面的东西替换成target的目标服务器url的，并且自己为空==
