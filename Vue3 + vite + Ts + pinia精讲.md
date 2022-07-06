# Vue3 + vite + Ts + pinia

教程：https://www.bilibili.com/video/BV1dS4y1y7vd?p=4&spm_id_from=333.788.header_right.history_list.click

![image-20220705071400219](Typora_images/Vue3 + vite + Ts + pinia精讲/image-20220705071400219.png)



# 1、环境搭建

```bash
npm init vite@latest
```

**==<font color='purple'>在指定的目录下使用这行命令，就能快速的创建一个vite项目了，这个vite应该是我用过的最快的项目构建工具了！</font>==**

![image-20220705075044767](Typora_images/Vue3 + vite + Ts + pinia精讲/image-20220705075044767.png)

## 1.1、三个调试命令

```json

  "scripts": {
    "dev": "vite",
    "build": "vue-tsc --noEmit && vite build",
    "preview": "vite preview"
  },
```

- *命令一：启动开发服务器*
- *命令二：为生产环境打包*
- *命令三：本地预览给生产环境打的包*

## 1.2、vite优势

- 真的很快，要比vue-cli快很多很多！



# 2、NVM、NRM

## 2.1、NVM

- NVM全称就是node.js version management，也就是node的版本管理工具，可以通过这个工具来切换和安装不同版本的node.js
- windows版本下载：https://github.com/coreybutler/nvm-windows/releases

**步骤一：下载安装包**

![image-20220706204437946](Typora_images/Vue3 + vite + Ts + pinia精讲/image-20220706204437946.png)

**步骤二：运行安装程序**

![image-20220706204538863](Typora_images/Vue3 + vite + Ts + pinia精讲/image-20220706204538863.png)





**步骤三：配置镜像（不配置镜像的话，根本没办法下载nodejs的..）**

![image-20220706204905481](Typora_images/Vue3 + vite + Ts + pinia精讲/image-20220706204905481.png)

配置内容如下

```bash
node_mirror: https://npm.taobao.org/mirrors/node/
npm_mirror: https://npm.taobao.org/mirrors/npm/
```

步骤四：使用nvm --help查看命令帮助，然后下载想要的nodejs版本即可。

**<font color='purple'>nvm切换Node环境的原理：就是把所有版本的nodejs安装包都下载到一个文件夹里面，然后再使用bash切换环境变量中的node路径就行了。</font>**

### 2.1.1、nvm use乱码问题

**<font color='purple'>出现乱码是因为cmd的权限不够，使用管理员权限打开cmd然后再nvm use 版本号就行了捏！</font>**





## 2.2、NRM

**介绍：nrm是npm源管理器，允许你在多个npm下载源直接快速切换使用。**

- 下载安装

```bash
npm install nrm -g
```



- 查看所有的源：-》

```bash
nrm ls
```

![image-20220706210510412](Typora_images/Vue3 + vite + Ts + pinia精讲/image-20220706210510412.png)

- 指定源：-》

```bash
nrm use taobao
```

## 2.3、认识目录和SFC

- 下面来讲解一下vite项目文件目录结构

![image-20220706214654547](Typora_images/Vue3 + vite + Ts + pinia精讲/image-20220706214654547.png)

- public目录：
  - public目录存放不需要编译的文件，比如图片和js文件
- src/assets目录：
  - 存放可以被编译的静态文件，存放在这里的图片会被编译   
- 可以在main.ts文件中存放公共API的
- **<font color='purple'>index.html，这个比较重要的，因为它是vite项目的入口文件，像webpack、rollup这些他们的入口文件都是main.js而不是html</font>**

- **<font color='violet'>tsconfig.json：ts的配置文件</font>**

```json
{
  "compilerOptions": {
    "target": "esnext",
    "useDefineForClassFields": true,
    "module": "esnext",
    "moduleResolution": "node",
      /** 严格模式这些东西...*/
    "strict": true,
    "jsx": "preserve",
    "sourceMap": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "esModuleInterop": true,
    "lib": ["esnext", "dom"],
    "skipLibCheck": true
  },
  "include": ["src/**/*.ts", "src/**/*.d.ts", "src/**/*.tsx", "src/**/*.vue"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```

- **<font color='violet'>vite.config.js vite的配置文件</font>**

```json
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vitejs.dev/config/
export default defineConfig({
    // 使用vue()插件来编译vue项目
  plugins: [vue()]
})
```

## 2.4、npm run dev启动vite项目原理

首先在vite的源码下，它的json配置中，配置了在bin目录下有一个vitejs文件

![image-20220706220534970](Typora_images/Vue3 + vite + Ts + pinia精讲/image-20220706220534970.png)

**==<font color='blue'>然后在 npm run dev的时候，会去.bin目录下找到vite脚本并运行，如下：</font>==**

![image-20220706220913076](Typora_images/Vue3 + vite + Ts + pinia精讲/image-20220706220913076.png)

**==<font color='purple'>我们可以看到.cmd脚本中有执行vite.js的命令了，所以当脚本运行的时候，vite项目就启动了！</font>==**



## 2.5、vue3配套插件

- 在vue2中有一款插件，就是vetur这个东西，这个插件可以帮助写vue代码的时候给一些提示，不过vue3中这个插件就没有用了。。。
- vue3中使用的是volar插件来进行vue代码的提示。（注意在使用两个插件中的一个的时候请禁用另一个插件）

![image-20220706223630097](Typora_images/Vue3 + vite + Ts + pinia精讲/image-20220706223630097.png)

安装这两个插件后，还会出现两个小功能

![image-20220706224208565](Typora_images/Vue3 + vite + Ts + pinia精讲/image-20220706224208565.png)

==右边的是预览preview功能，左边的是分块功能，就是可以把逻辑代码和template分开这样子==

























