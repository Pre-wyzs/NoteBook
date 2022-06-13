# Vue3.0 + Vite 极速上手

# 1、基础部分

## 1.1、vue3新特性

### 1.1.1、v-for获取ref dom对象数组的变化

案例：

#### **vue2获取v-for的doms**

```vue
<template>
    <div>
        <ul>
            <li v-for="(item) in data" :key="item.id" ref="person">{{item.name}}</li>
        </ul>
    </div>
</template>
<script>

export default {
  name: 'GetDoms',
  data () {
    return {
      data: [
        {
          id: 1,
          name: 'zzw'
        },
        {
          id: 2,
          name: 'xujie'
        },
        {
          id: 3,
          name: 'hyf'
        }
      ]
    }
  },
  methods: {
    getPerson () {
      console.log(this.$refs.person)
    }
  },
  mounted () {
    this.getPerson()
  }
}
</script>
<style scoped>

</style>

```

**输出：**

![image-20220611103728686](Typora_images/Vue3.0 + Vite 极速上手/image-20220611103728686.png)

==虽然这样也能获取，但是会出现bug不太容易修改！==



#### vue3获取v-for的doms

```vue
<template>
    <div>
        <ul>
            <li v-for="(item) in data" :key="item.id" :ref="person">{{item.name}}</li>
        </ul>
    </div>
</template>
<script>

export default {
  name: 'GetDoms',
  data () {
    return {
      data: [
        {
          id: 1,
          name: 'zzw'
        },
        {
          id: 2,
          name: 'xujie'
        },
        {
          id: 3,
          name: 'hyf'
        }
      ],
      persons: []
    }
  },
  methods: {
    person (el) {
        this.persons.push(el)
    },
    getPerson () {
        console.log(this.persons);
    }
  },
  mounted () {
    this.getPerson();
  }
}
</script>
<style scoped>

</style>
```

**==<font color='red'>原理：vue3在这个方面做了很大的改善，并且这些改进不是向下兼容的！它把ref绑定了一个methods中的函数，然后参数就是每一项的dom，可以把这些dom push到一个数组中，然后就可以任意使用这些dom了</font>==**



### 1.1.2、$children的新变化

**<font color='red'>在vue3.0中，把$children属性去除了，如果想要获取到子组件对象，从而访问子组件的方法和属性，可以在使用子组件的时候添加一个 ref; 然后使用this.$refs.ref名称就可以获取到子组件的对象了</font>**

```vue
<template>
    <div>
        <Child ref="child" msg="你好章子唯"/>
    </div>
</template>
<script>
import Child from './Child.vue'

export default {
    name: 'Father',
    components: {
        Child
    },
    mounted () {
        console.log(this.$refs.child);
    }
}
</script>
<style scoped>

</style>
```

输出：
![image-20220611141429008](Typora_images/Vue3.0 + Vite 极速上手/image-20220611141429008.png)



**==<font color='red'>如果使用this.$refs就可以获取到所有的ref dom对象了</font>==**

```vue
<template>
    <div>
        <Child ref="child" msg="你好章子唯"/>
        <div ref="wmy">魏梦莺</div>
    </div>
</template>
<script>
import Child from './Child.vue'

export default {
    name: 'Father',
    components: {
        Child
    },
    mounted () {
        console.log(this.$refs);
    }
}
</script>
```

输出：
![image-20220611142134427](Typora_images/Vue3.0 + Vite 极速上手/image-20220611142134427.png)



### 1.1.3、vue3.0插槽新变化

- 在vue3中，移除了slot 和 slot-scope两个属性，直接使用 v-slot就行了。



### 1.1.4、响应式系统的更新

**<font color='red'>在vue2中，通过定位数组下标，从而改变数组中某一项的值是不行的。可以说是一个很严重的Bug了</font>**

```vue
<template>
    <div>
        <ul>
            <li v-for="(v,k) in men" :key="k">{{v}}</li>
        </ul>
        <button @click="changeItem">改变数组</button>
    </div>
</template>
<script>

export default {
  name: 'Test',
  data () {
    return {
      men: [
        { id: 1, name: '路飞-v2' },
        { id: 2, name: '鸣人-v2' }
      ]
    }
  },
  methods: {
    changeItem () {
      this.men[1] = { id: 2, name: '许洁-v2' }
    }
  }
}
</script>

```

在vue3中就可以了：

![image-20220611172342961](Typora_images/Vue3.0 + Vite 极速上手/image-20220611172342961.png)

点击后是可以的：

![image-20220611172410172](Typora_images/Vue3.0 + Vite 极速上手/image-20220611172410172.png)

具体的原理比较复杂，目前的我反正是看不懂的：参考

https://www.bilibili.com/video/BV1yK4y1M7Fz?p=5&vd_source=365d13057e58bb6a007cdd5275785229



### 1.1.5、Compesition API

```vue
<template>
    <div>
        <div>{{nu}}</div>
        <button @click="addNu(3)">增加一个数</button>
        <div>{{person.name}}</div>
        <button @click="setPersonName('ty')">改变人的姓名</button>
    </div>
</template>
<script>
import { defineComponent, ref, reactive } from 'vue'

export default defineComponent({
    setup() {
        //ref是用来维护响应式的普通变量的，很少会用到一般开发中都是使用reactive的
        const nu = ref(2)

        //reactive是用来维护响应式的对象，数组的
        const person = reactive({
            id: 1,
            name: 'zzw',
            sex: 1,
            age: 23
        })

        const setPersonName = (setName) => {
            person.name = setName;
        }

        const addNu = (nu1) => {
            nu.value = nu.value + nu1;
        }

        return {
            nu,
            person,
            setPersonName,
            addNu
        }

    },
    mounted () {
        console.log('你好')
    }
})

</script>
<style scoped>

</style>
```

**==<font color='red'>使用reactive函数来维护 对象，数组的响应变化；注意在setup函数中定义新的函数，不能使用 setName () {...}这样的方式，不然会报错的，要么使用原生js的 function来定义，要么使用箭头函数来定义；</font>==**



### 1.1.6、setUp级别的生命周期函数

- setUp函数在组件被创建之前就执行了。。。

![image-20220611180935000](Typora_images/Vue3.0 + Vite 极速上手/image-20220611180935000.png)

所以在setUp函数中是访问不到this的

```vue
<template>
    <div>
        <div>{{nu}}</div>
        <button @click="addNu(3)">增加一个数</button>
        <div>{{person.name}}</div>
        <button @click="setPersonName('ty')">改变人的姓名</button>
    </div>
</template>
<script>
import { defineComponent, ref, reactive } from 'vue'

export default defineComponent({
    setup() {
        console.log(this)

        //ref是用来维护响应式的普通变量的，很少会用到一般开发中都是使用reactive的
        const nu = ref(2)

        //reactive是用来维护响应式的对象，数组的
        const person = reactive({
            id: 1,
            name: 'zzw',
            sex: 1,
            age: 23
        })

        const setPersonName = (setName) => {
            person.name = setName;
        }

        const addNu = (nu1) => {
            nu.value = nu.value + nu1;
        }

        return {
            nu,
            person,
            setPersonName,
            addNu
        }

    },
    created () {
        console.log('--created--',this)
    },
    mounted () {
        console.log('--mounted--',this)
    }
})

</script>
<style scoped>

</style>

```

打印结果：
![image-20220611181415376](Typora_images/Vue3.0 + Vite 极速上手/image-20220611181415376.png)

**==<font color='red'>那访问不到this怎么能在mounted，created这些钩子中调用方法，完成对组件数据的初始化和特殊操作呢？在设计setUp的时候他们也考虑到了这个问题，很简单，在setUp中有对应于vue对象创建阶段钩子函数的方法的：</font>==**

![image-20220611183822333](Typora_images/Vue3.0 + Vite 极速上手/image-20220611183822333.png)

**又因为这些方法不都是定义在setUp中的吗，直接调用就行了，需要注意的是setUp钩子函数需要引入使用！**

```vue
<template>
    <div>
        <div>{{nu}}</div>
        <button @click="addNu(3)">增加一个数</button>
        <div ref="fook">{{person.name}}</div>
        <button @click="setPersonName('ty')">改变人的姓名</button>
    </div>
</template>
<script>
import { defineComponent, ref, reactive, onMounted } from 'vue'

export default defineComponent({
    setup() {
        onMounted (() => {
            //把这个数据想象为就是从后端获取到的
            const name =  '许洁';

            console.log('--setUp onMounted--',setPersonName(name));
        }) 

        //ref是用来维护响应式的普通变量的，很少会用到一般开发中都是使用reactive的
        const nu = ref(2)

        //reactive是用来维护响应式的对象，数组的
        const person = reactive({
            id: 1,
            name: 'zzw',
            sex: 1,
            age: 23
        })

        const setPersonName = (setName) => {
            person.name = setName;
        }

        const addNu = (nu1) => {
            nu.value = nu.value + nu1;
        }

        return {
            nu,
            person,
            setPersonName,
            addNu
        }

    },
    created () {
        console.log('--created--',this)
    },
    mounted () {
        console.log('--mounted--',this)
    }
})

</script>
<style scoped>

</style>

```



## 1.2、基于Vite构建vue3项目

vite官网：https://vitejs.cn/guide/#scaffolding-your-first-vite-project



- webpack打包的过程：

![image-20220611185623133](Typora_images/Vue3.0 + Vite 极速上手/image-20220611185623133.png)

![image-20220611185719635](Typora_images/Vue3.0 + Vite 极速上手/image-20220611185719635.png)

- **<font color='red'>就是传统webpack vue-cli都是经过先经过 编译，然后打包到内存（虽然在磁盘上看不到打包好的代码，但是内存中有！），然后才能进行运行和展示，这就会导致一个问题，你修改一个文件，整个项目就会被重新编译一遍，所以很耗费资源。</font>**

- 再来聊聊为什么需要打包，因为打包现在很多的js代码都是用ES7 ES8的语法的写的，而很多的浏览器根本就不支持这些语法，所以得使用打包工具把代码转成es5的，然后就是文件太分散了，需要打包。



vite原理：

![image-20220611190604772](Typora_images/Vue3.0 + Vite 极速上手/image-20220611190604772.png)

**<font color='red'>就是先启动开发服务器，然后也不用打包，只是服务器请求哪一块内容，就编译那一块的内容执行就完事了，节省了编译和打包的时间。</font>**

- vite在开发环境下，压根就不打包。。。



# 2、jsx语法

https://www.bilibili.com/video/BV1XV411d7SE?p=8&vd_source=365d13057e58bb6a007cdd5275785229

## 2.1、react安装

```bash
npm install create-react-app -g

#创建项目
create-react-app myreact
```



## 2.2、语法基础

```react
import './App.css';

function App() {
  return (
    <div className='App'>
      hello {2 + 3}
    </div>
  );
}

export default App;

```

**==<font color='red'>return 后面跟上一个()，括号里面只能有一个根元素，然后可以在{}中执行js的语法，类名的关键字是className，不是class了</font>==**



- **<font color='red'>1、行内样式可以直接展开</font>**

```react
import './App.css';

function App() {
  let style = { "font-family":"Italy", "color":"blue", "background-color":"black" };

  return (
    <div className='App' style={style}>
      hello {2 + 3}
    </div>
  );
}

export default App;

```

![image-20220612070800377](Typora_images/Vue3.0 + Vite 极速上手/image-20220612070800377.png)

2、注释使用 /**/写的

**<font color='red'>3、数组中可以直接写div节点</font>**

```react
import './App.css';

function App() {
  let style = { "font-family":"Italy", "color":"blue", "background-color":"black" };

  const arr = [
    <div>许洁</div>,
    <div>李宇涵</div>,
    <div>贺源峰</div>,
  ];

  return (
    <div className='App' style={style}>
      hello {2 + 3}
      {arr}
    </div>
  );
}

export default App;

```

![image-20220612071331582](Typora_images/Vue3.0 + Vite 极速上手/image-20220612071331582.png)











