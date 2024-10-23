# VUE组件传参

在 Vue 中，给组件传参可以通过props的方式进行。父组件向子组件传递参数时，需要在子组件中声明接收的 props，并在父组件中通过模板语法传递数据。

## 基本步骤：

	1.	在子组件中声明 props
	•	子组件需要通过 props 选项或 defineProps 来声明可以接收的参数。
	2.	在父组件中传递参数
	•	父组件通过属性的方式传递数据给子组件。

### 示例 1：普通传参

子组件（ChildComponent.vue)

```ts
<template>
  <div>
    <p>Message from parent: {{ message }}</p>
    <p>User name: {{ user.name }}</p>
  </div>
</template>

<script setup>
// 使用 defineProps 来声明 props
const props = defineProps({
  message: String,
  user: Object
});
</script>
```

父组件（ParentComponent.vue）

```ts
<template>
  <div>
    <ChildComponent message="Hello from parent!" :user="userData" />
  </div>
</template>

<script setup>
import ChildComponent from './ChildComponent.vue';

// 模拟数据
const userData = { name: 'Alice', age: 25 };
</script>
```

	•	传递字符串：message="Hello from parent!"
	•	传递对象：:user="userData" 这里使用 : 表示我们在传递 JavaScript 变量而非字符串。

### 示例 2：动态数据传递

你可以动态传递 props，父组件中传递的参数可以随着数据的变化而更新。

父组件（ParentComponent.vue）

```ts
<template>
  <div>
    <input v-model="dynamicMessage" placeholder="Enter a message">
    <ChildComponent :message="dynamicMessage" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import ChildComponent from './ChildComponent.vue';

// 定义动态数据
const dynamicMessage = ref('');
</script>
```

在这里，message 将根据父组件中的输入框的值实时更新。

### 示例 3：传递函数作为参数

你可以传递函数作为参数，子组件中可以调用父组件传递的函数。

子组件（ChildComponent.vue）

```ts
<template>
  <button @click="sendMessage">Send message to parent</button>
</template>

<script setup>
const props = defineProps({
  sendMessage: Function
});
</script>

父组件（ParentComponent.vue）

<template>
  <ChildComponent :sendMessage="handleMessage" />
</template>

<script setup>
function handleMessage() {
  alert('Message from child component!');
}
</script>
```

点击按钮时，子组件会调用父组件传递过来的 handleMessage 函数。

#### 小结：

	1.	传递静态或动态数据：可以通过v-bind（简写 :）传递数据或 JavaScript 变量。
	2.	传递事件或函数：可以将父组件的方法作为 props 传递给子组件。
	3.	组件通信：props 是从父到子组件通信的主要方式，子组件接收父组件传递的值并进行展示或操作。