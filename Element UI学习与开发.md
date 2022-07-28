# Element UI学习与开发

教程：https://www.bilibili.com/video/BV1QU4y1E7qo/?spm_id_from=333.788.recommend_more_video.0&vd_source=365d13057e58bb6a007cdd5275785229



yarn相对于npm的有点介绍：

![image-20220719230634808](Typora_images/Element UI学习与开发/image-20220719230634808.png)

![image-20220719230708504](Typora_images/Element UI学习与开发/image-20220719230708504.png)

![image-20220719230738507](Typora_images/Element UI学习与开发/image-20220719230738507.png)































# 组件封装与组件库搭建

教程：https://www.bilibili.com/video/BV1nJ411V75n?p=3&vd_source=365d13057e58bb6a007cdd5275785229

# 1、Button组件封装

```vue
<template>
    <div class="my-button">黑马组件</div>
</template>
<script>
    export default {
        name: 'MyButton'
    }
</script>
<style lang="scss">

</style>
```

**==在vue3中注册全局组件的方法：具体看官网文档就行==**

```js
import { createApp, VueElement } from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'
/** 全局注册组件 */
import MyButton from './components/Button'
const app = createApp(App)
app.component(MyButton.name, MyButton)

app.use(store).use(router).mount('#app')
```

**<font color='deepred'>在vue3中，不在直接使用Vue.component来注册组件了，而是使用createApp创建的实例对象的component方法来注册组件，参数一是组件的名字，可以直接指定一个字符串，参数二是要注册到全局的组件了。</font>**

```vue
<template>
  <div id="nav">
    <my-button></my-button>
  </div>
</template>

<style>
</style>
```

**==<font color='red'>组件注册到全局后，在任何地方都可以随意的调用了。</font>==**















