



# component-encapsulation

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```

# 一.用vite创建项目

- ```cmd
  npm init vue@latest
  ```

- ```cmd
  D:\workspace>npm init vue@latest
  
  Vue.js - The Progressive JavaScript Framework
  
  √ Project name: ... vue-vite-project01
  √ Add TypeScript? ... No / Yes
  √ Add JSX Support? ... No / Yes
  √ Add Vue Router for Single Page Application development? ... No / Yes
  √ Add Pinia for state management? ... No / Yes
  √ Add Vitest for Unit Testing? ... No / Yes
  √ Add Cypress for both Unit and End-to-End testing? ... No / Yes
  √ Add ESLint for code quality? ... No / Yes
  √ Add Prettier for code formatting? ... No / Yes
  
  Scaffolding project in D:\workspace\vue-vite-project01...
  
  Done. Now run:
  
    cd vue-vite-project01
    npm install
    npm run lint
    npm run dev
  
  
  D:\workspace>cd vue-vite-project01
  
  D:\workspace\vue-vite-project01>npm install
  
  added 329 packages in 1m
  
  D:\workspace\vue-vite-project01>
  
  ```

- **问题：**

- # App.vue Doctor

- ### ❗ `vue-tsc` version different

- The `Vue Language Features (Volar)` version is `1.0.8`, but workspace `vue-tsc` version is `0.40.13`, there may have different type checking behavior.

- **解决：**升级 vue-tsc 版本

- ```cmd
  npm i vue-tsc@latest -D
  ```

  

# 二、打包上线

```cmd
npm run build
```



# 三、Vite打包后的dist不能直接在浏览器

## **方案一：**

### 1.原因

Vite 本身依赖于[原生ES模块](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)来做模块加载，而原生ES模块是不支持 `file://` 本地访问的。

### 2.解决办法

**方案一：使用http-server插件启动**

1.安装node.js；（已安装跳过）

2.安装http-server。

```coffeescript
npm install http-server -g
```

或

```sql
yarn global add http-server
```

3、进入dist根目录执行启动项目

```vbscript
http-server
```



## **方案二：使用nginx启动**

1、把dist拷贝至nginx的html目录下（其他目录也行，需在nginx里配置root）；

![img](https://img-blog.csdnimg.cn/c122b32211da4af9b86b3f1e66af2197.png)

2、配置nginx.conf

![img](https://img-blog.csdnimg.cn/88d0de2bbc7341dcb3a49f08e74c3b9e.png)

 3、保存并启动nginx，访问http://127.0.0.1:3000即可。

# 四、element-plus

### 1.安装

```cmd
npm install element-plus --save
```

### 2.Volar 支持[#](https://element-plus.gitee.io/zh-CN/guide/quickstart.html#volar-支持)

如果您使用 Volar，请在 `tsconfig.json` 中通过 `compilerOptions.type` 指定全局组件类型。

```
// tsconfig.json
{
  "compilerOptions": {
    // ...
    "types": ["element-plus/global"]
  }
}
```

### 3.按需导入[#](https://element-plus.gitee.io/zh-CN/guide/quickstart.html#按需导入)

您需要使用额外的插件来导入要使用的组件。

#### 自动导入推荐[#](https://element-plus.gitee.io/zh-CN/guide/quickstart.html#自动导入-推荐)

首先你需要安装`unplugin-vue-components` 和 `unplugin-auto-import`这两款插件

```cmd
npm install -D unplugin-vue-components unplugin-auto-import
```

然后把下列代码插入到你的 `Vite` 或 `Webpack` 的配置文件中

##### Vite[#](https://element-plus.gitee.io/zh-CN/guide/quickstart.html#vite)

```ts
// vite.config.ts
import { defineConfig } from 'vite'
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'

export default defineConfig({
  // ...
  plugins: [
    // ...
    AutoImport({
      resolvers: [ElementPlusResolver()],
    }),
    Components({
      resolvers: [ElementPlusResolver()],
    }),
  ],
})
```

### 4.App.vue中引入element

```ts
<template>
  <div>  
    <el-row class="mb-4">
      <el-button>Default</el-button>
      <el-button type="primary">Primary</el-button>
    </el-row>    
  </div>
</template>
```



### 5.重启项目

```cmd
npm run dev
```

# 五、配置路由

## 1.src>router>index.ts

```ts
import { createRouter, createWebHistory } from "vue-router";

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: "/",
      redirect: "/home",
    },
    {
      path: "/home",
      name: "home",
      component: () => import("../views/HomeView.vue"),
    },
    {
      path: "/about",
      name: "about",
      // route level code-splitting
      // this generates a separate chunk (About.[hash].js) for this route
      // which is lazy-loaded when the route is visited.
      component: () => import("../views/AboutView.vue"),
    },
  ],
});

export default router;

```

## 2.App.vue

```ts
<template>
  <div>    
    <RouterLink to="/home">首页</RouterLink>
    <RouterLink to="/about">关于</RouterLink>
    <RouterView></RouterView>
  </div>
</template>
```



# 六、编写代码

## 1.App.vue

```vue
<template>
  <div>
    <h1>{{ msg }}</h1>
    <HelloWorld />
  </div>
</template>

<script setup lang="ts">
import HelloWorld from "./components/HelloWorld.vue";
const msg = "Hello App";
</script>

<style scoped></style>

```

## 2.src>main.ts 中导入样式表

```ts
import "./assets/main.css"
```

## 3.src>assets>main.css

```javascript
@import "./base.css";

#app {
  max-width: 1280px;
  /* margin: 0 auto; */
  padding: 1rem;
  font-weight: normal;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
  }

  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }
}

```



## 4. vue3.0之组件通信详解(defineProps、defineEmits、defineExpose)



 我们在做vue项目中，我们总会遇到组件引入，在嵌套组件中我们的父级组件中引入子级组件中的值，或者在子组件中我们使用父组件中的值。那么当我们遇到这样的场景我们应该怎么做，在vue2.0中，我们使用props和emit进行父子之间的通信，兄弟之间用事件中央总线(event bus)；在vue3.2的语法中我们则使用defineProps和defineEmits来声明props和emit，用其进行组件之间的传值，那么接下来，我们来看看。

**defineProps：**

​    1、用于组件通信中父级组件给子级组件传值，其用来声明props,其接收值为props选项相同的值

​    2、默认支持常见的类型检查，在ts下，我们需要明确变量的类型，类型经常是我们的自定义类型

​    3、只能在<script setup>中使用

​    4、不需要被导入即可使用,它会在编译<script setup>语法块时一同编译掉

​    5、必须在<script setup>的顶层使用，不可以在<script setup>的局部变量中引用

​    6、不可以访问 <script setup> 中定义的其他变量，因为在编译时整个表达式都会被移到外部的函数中

```vue
// 父级组件使用自定义属性向下传递值
<div class="home">
  <HelloWorld :msg="msg"/>
</div>
<script setup>
import HelloWorld from '@/components/HelloWorld'
/**
* 父级组件传递一个自定义属性
* 和props传递方式一样
* @type {string}
*/
const msg = '张三';
</script>
// 子级组件使用defineProps接收值
<div class="hello">
  <h1>{{ props.msg }}</h1>
</div>
<script setup>
/**
* 无需导入直接使用
* 写在<script setup>里面
* defineProps传入的对象key值就是传递的属性，父级传入msg，那么子级接收msg，定义其类型
* @type {Readonly<ExtractPropTypes<{msg: StringConstructor}>>}
* 以下props就是defineProps返回的对象
*/
const props = defineProps({
  msg: String,
});
</script>
<script setup>
/**
* 如果写在局部
* 报错：Uncaught ReferenceError: defineProps is not defined*/
const btn = function (){
  const props = defineProps({
    msg: String,
  });
}
</script>
```

**实例**

```vue
//父组件
<template>
  <div class="home">
    <AButton :type="type">{{type}}</AButton>
  </div>
</template>

<script setup>
import AButton from "../components/button/AButton.vue";

const type = "success";
</script>

<style lang="scss" scoped></style>

```

```vue
//子组件
<template>
  <h1>父组件传入的数据：{{props.type}}</h1>
  <h1>子组件处理后的数据：{{theme}}</h1>
  <button class="a-button" :class="theme">
    <slot />
  </button>
</template>

<script setup>
import { computed } from "@vue/reactivity";

const props = defineProps({
  type: String,
});
const theme = computed(() => `a-button-${props.type}`);
console.log(theme);
</script>

```

## 5. vue3 defineEmits <setup>语法糖写法

> 子组件接收父级组件中定义的事件

```dart
//父级组件定义update-list事件
<Operate :param="scope.row.id" @update-list="getList()" />
//=============================================
//子组件Operate接收updateList事件 使用驼峰方式书写
const emits = defineEmits(['updateList']);
//子组件中调用方法
emits('updateList')
```

> 子组件接收参数

```tsx
const props = defineProps({
  params: {
    type: Object,
    default: () => { }
  },
  flag: {
    type: Number,
    default: 0
  }
})
// 动态数据
const { params } = toRefs(props)
```

> 子组件向父级暴露函数

```csharp
const getUserList = () => {
  //.......
}
defineExpose({
  getUserList
})

//父级方法中调用

<Child ref="child" />
.....
const child= ref()
child.value.getUserList()
```

> 监听父级参数

```tsx
const props = defineProps({
  detailInfo: {
    type: Object,
    default: () => { }
  },
})
const { detailInfo } = toRefs(props);


watch([props], () => {
  // show.value = true;
  console.log(detailInfo.value, 'detailInfo.value');
  // if (!detailInfo.value.dealFlag || detailInfo.value.dealFlag == 0) update({ id: detailInfo.value.id, dealFlag: 1 }, 'flag')
});
```

## 6. button 按钮实现 loading 效果

>   方法一

```vue
//父组件 通过 :before-change 向子组件传入 asyncFunction 函数
<template>
<AButton type="success" :before-change="asyncFunction">默认按钮</AButton>
</template>

<script setup>
...
const asyncFunction = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve();
    }, 3000);
  });
};
</script>

```

```vue
//子组件通过宏函数 defineProps()接收 beforeChange
<script setup>
const props = defineProps({
  ...
  beforeChange: Function,
});

//通过change 处理
const load = ref(false);
const change = () => {
  if (typeof props.beforeChange === "function") {
    load.value = true;
    props
      .beforeChange()
      .then((response) => {
        load.value = false;
      })
      .catch(() => {
        load.value = false;
      });
  }
</script>
    
//通过控制load的值 从而改变loading状态
<template>
  <button
    @click="change"
    class="a-button"
    :class="[vtype, isBorder, isRound, vsize, blockCss]"
    :disabled="disabled || loading || load"
    :style="[minWidthCss]"
  >
    <span>
      <i v-if="loading || load" class="iconfont icon-prefix icon-loading"></i>
      <i v-if="iconPrefix" class="iconfont icon-prefix" :class="iconPrefix"></i>
      <slot />
      <i v-if="iconSuffix" class="iconfont icon-suffix" :class="iconSuffix"></i>
    </span>
  </button>
</template>


```

> 方法二
>

```vue
// 父组件 监听子组件发射的parent-click 事件，接收后通过 handlerClick 处理
//通过flag的值 调整loading状态
<template>  
    <AButton :loading="flag" @parent-click="handlerClick">默认按钮</AButton>
<template> 

<script setup>
import { ref } from "vue";

const flag = ref(false);  
const handlerClick = (data) => {
  console.log(data);
  flag.value = true;
  setTimeout(() => {
    flag.value = false;
    console.log("现在可以重新点击");
  }, 3000);
};  
</script>
  
```



```vue
//子组件
<script setup>
// 定义一个子传父事件-parentClick
const emits = defineEmits(["parentClick"]);
  
// 点击按钮时候通过change方法将parentClick 发射给父组件
const change = () => emits("parentClick",'我是子组件传递的信息');
</script>

<template>
  <button
    @click="change"
    class="a-button"
    :class="[vtype, isBorder, isRound, vsize, blockCss]"
    :disabled="disabled || loading || load"
    :style="[minWidthCss]"
  >
    <span>
      <i v-if="loading || load" class="iconfont icon-prefix icon-loading"></i>
      <i v-if="iconPrefix" class="iconfont icon-prefix" :class="iconPrefix"></i>
      <slot />
      <i v-if="iconSuffix" class="iconfont icon-suffix" :class="iconSuffix"></i>
    </span>
  </button>
</template>
```









# 七、问题

### 1.文本中每行都有Delete `␍`

使用VSCode开发Vue3项目，编辑的文本中每行都有Delete `␍`eslint(prettier/prettier)错误，查找原因发现是Windows系统下，按回车时插入回车和换行CRLF两个符号，而这在eslint看来是警告错误，解决办法是在.eslintrc.cjs中增加配置，说明这种情况不是错误：

```js
"rules": {
"prettier/prettier": ["error", { "endOfLine": "auto" }]
}
```

### 2.【VUE】报错:Component name “Login“ should always be multi-word.

报错：[Component](https://so.csdn.net/so/search?q=Component&spm=1001.2101.3001.7020) name “Login” should always be multi-word.意思是说组件名"Login"应该总是多个单词，其实就是eslint报出我的组件名称命名不规范，应该采用驼峰命名法。

解决：可以将组件名称改成 LoginView.vue

### 3.格式化时间并实时显示

3.1 src/utils/formateDate.ts

```ts
const complement = function (value: any) {
  return value < 10 ? `0${value}` : value;
};

export const formateDate = (date: any) => {
  const time = new Date(date);
  const year = time.getFullYear();
  const month = complement(time.getMonth() + 1);
  const day = complement(time.getDate());
  const hour = complement(time.getHours());
  const minute = complement(time.getMinutes());
  const second = complement(time.getSeconds());
  const week = "星期" + "日一二三四五六".charAt(time.getDay());
  return `${year}年${month}月${day}日 ${week} ${hour}:${minute}:${second}`;
};

```

3.2 src/components/header/DateTime.vue

```ts
<template>
  <div id="clock">{{ date }}</div>
</template>

<script lang="ts" setup>
import { formateDate } from "@/utils/formatterData";
import { ref, onMounted } from "vue";
const date = ref("");
onMounted(() => {
  setInterval(() => {
    getDate();
  }, 1000);
});

const getDate = function () {
  date.value = formateDate(new Date());
};
</script>

<style scoped></style>
```

### 4.Vite+Vue项目添加sass预处理器



##### 一：安装[sass](https://so.csdn.net/so/search?q=sass&spm=1001.2101.3001.7020)

vite有内置的sass配置信息，所以直接安装sass即可

```
npm install --save-dev sass
1
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/1c6b5352c7dd48808894fb7090ef710c.png)

##### 二：编写全局css变量/全局mixin

在assets文件夹下创建scss目录，添加globalMixin.scss和globalVar.scss文件

![在这里插入图片描述](https://img-blog.csdnimg.cn/936d9e20a24e49f5b047eac0c71c8d46.png)

添加几个案例

```css
//globalVar.scss
$bg-color: #1989fa;


//globalMixin.scss
@mixin box-shadow($bulr: 20px, $color: #1989fa7a) {
  -webkit-box-shadow: 0px 0px $bulr $color;
  -moz-box-shadow: 0px 0px $bulr $color;
  box-shadow: 0px 0px $bulr $color;
}
12345678910
```

##### 三：引入

###### 全局引入

打开项目目录下vite.config.js文件，添加配置信息

```javascript
 //配置sass
css: {
    preprocessorOptions: {
      scss: {
        // '@import "assets/scss/globalVar.scss";@import "assets/scss/globalMixin.scss";'
        additionalData:
          '@import "../src/assets/scss/globalVar.scss";@import "../src/assets/scss/globalMixin.scss";',
      },
    },
  },
```

如图

![在这里插入图片描述](https://img-blog.csdnimg.cn/00dbbb9adbff47bb9599629a877b799e.png)

直接使用即可

![在这里插入图片描述](https://img-blog.csdnimg.cn/aebb7b08e9a04df29c92b5f1c362b296.png)

###### 按需引入

在需要使用的style里import引入即可使用

![在这里插入图片描述](https://img-blog.csdnimg.cn/d09c35f579034c869088ccb0574f6ee6.png)

##### 四：注意事项

**使用sass的时候，是使用`lang=scss`并不是`lang=sass`，否则样式会失去高亮且代码报错**

![在这里插入图片描述](https://img-blog.csdnimg.cn/1b6dd12edcab496c8c5c2af6015fde46.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/06db2316d22b4c9e995a87bf3345a6b1.png)
over~

### 5.Clone Github失败的解决全过程

清除代理设置：命令如下：

​		

```cmd
git config --global --unset http.proxy

git config --global --unset https.proxy
```

### 6. Git报错解决：OpenSSL SSL_read: Connection was reset, errno 10054

**6-1.首先检查C盘下host文件中的github相关访问的域名对应的ip是否正确**

- hosts文件目录：C:\Windows\System32\drivers\etc

- ip地址查询：https://www.ipaddress.com/
  查询下面三个域名ip：
  github.com
  github.global.ssl.fastly.net
  codeload.Github.com

  

**6-2.找到hosts文件，将上述三行（带ip）放在末尾，保存。**



127.0.0.1 powerservice.csii.com.cn

140.82.114.4 github.com

140.82.113.10 codeload.Github.com

**6-3. cmd刷新DNS： ipconfig /flushdns**

**6-4. IP地址没有问题的情况下，多上传几次。**

**6-5. 若前面两步都没有用，修改设置，解除ssl验证。**
进入Git Bash Here

```cmd
git config --global http.sslVerify "false"
```

再次尝试git



### 7. -webkit-keyframes 动画抖动问题

```
@-webkit-keyframes loading {

 0% {

  -webkit-transform: rotate(0deg);

 }

 100% {

  -webkit-transform: rotate(360deg);

 }

}
```

