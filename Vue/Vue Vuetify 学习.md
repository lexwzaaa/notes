# Vue Vuetify 学习 

## 项目创建

* 首先命令行创建项目

```sh
npm create vuetify@latest
```

* 然后需要进行一些配置

```sh
Need to install the following packages:
create-vuetify@2.2.6
Ok to proceed? (y) y


> npx
> create-vuetify


Vuetify.js - Material Component Framework for Vue

✔ Project name: … MyPage
✔ Which preset would you like to install? › Default (Adds routing, ESLint & SASS variables)
✔ Use TypeScript? … No / Yes
✔ Would you like to install dependencies with yarn, npm, pnpm, or bun? › npm
✔ Install Dependencies? … No / Yes
```

## 项目分析
具体项目大部分都是常规设置，但是有几个需要注意的地方：

1. 项目使用了自动配置路由：
	
	项目使用的是unplugin-vue-router这个插件来自动配置路由而不用繁琐的手动写路由json对象，他可以根据src/pages下的文件来自动映射出相对的路由。
	[插件具体使用说明](https://uvr.esm.is/introduction)
### 	例子

	
	```sh
	src/pages/
	├── index.vue
	├── about.vue
	└── users/
      ├── index.vue
   	  └── [id].vue
	```
	
	这个目录结构生成的路由是这样的：
	* / : -> 渲染 index.vue
	* /about : -> 渲染 about.vue
	* /users : -> 渲染 users/index.vue
	* /users/:id : -> 渲染 users/[id].vue ， id 会变成路由参数 注意，经过测试，实际渲染成的路由为 /users/[id]
	
	然后传参的话需要这么传
	
	```ts
	<router-link :to="{ name: '/users/[id]',params:{id: user.id}}">
  		...
	</router-link>
	```

	
2. Vuetify 内置了很多样式工具类，工具类可以联合使用。用空格隔开即可。这个不了解可能看代码会有障碍

	```ts
	<div class="py-4 md-1 mt-2 ..."/>
	```

	[各种工具类说明](https://vuetifyjs.com/zh-Hans/styles/borders/#section-4f7f7528)
	### [Vuetify官网](https://vuetifyjs.com/zh-Hans/)
