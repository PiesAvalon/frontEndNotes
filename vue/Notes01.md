# Notes01-项目 setup 响应式（ref rective）
## 创建项目
```bash
npm create vue@latest
```
启动项目
```bash
cd <your-project-name>
npm install
npm run dev
```

## 关于setup语法
### setup函数
setup 是 Vue 3 Composition API 中的一个特殊函数。它在组件实例创建之前执行，用于设置组件的响应式状态、计算属性、方法等。setup 函数在 beforeCreate 和 created 生命周期钩子之前执行。  
beforeCreate 是 Vue 生命周期中的一个钩子函数，它在组件实例被创建之前执行。在这个阶段，组件的 data、methods、computed 等属性还没有被初始化。
```vue
<script>
export default{
  setup(){
    console.log('setup')
  },
  beforeCreate(){
    console.log('before create')
  }
}
</script>
```
### 箭头函数
箭头函数（Arrow Function）是 ​ES6（ECMAScript 2015）​ 引入的一种更简洁的函数定义语法。
```js
const sayHello = () => console.log("Hello!");
```
```js
const numbers = [1, 2, 3, 4];

// 传统函数
const doubledTraditional = numbers.map(function(num) {
  return num * 2;
});

// 箭头函数
const doubledArrow = numbers.map(num => num * 2);

console.log(doubledTraditional); // 输出: [2, 4, 6, 8]
console.log(doubledArrow); // 输出: [2, 4, 6, 8]
```
```js
    const message = "this is a message"
    const logMessage = () =>{
      console.log(message)
    }
```
箭头函数可以用return显示返回值
```js
const add = (a, b) => {
  return a + b; // 显式返回 a + b 的结果
};

console.log(add(2, 3)); // 输出: 5
```
也可以通过不加{}来隐式返回值
```js
const add = (a, b) => a + b; // 隐式返回 a + b 的结果
console.log(add(2, 3)); // 输出: 5
```
### setup的返回值
setup函数return出来的变量可以在template中用  
切记：vue3中不使用this, this不再指向组件实例
```js
<script>
export default{
  setup(){
    console.log('setup')
    const message = "this is a message"
    const logMessage = () =>{
      console.log(message)
    }
    return {message, logMessage}//记住一定要返回出来！
  },
  beforeCreate(){
    console.log('before create')
  }
}
</script>
<template>
  <div>
    <h1>Vue 3</h1>
    <h2>{{ message }}</h2>
    <button @click="logMessage">click this buton! </button>
  </div>
</template>
```
### script setup写法
setup语法糖，效果和上面的setup函数一样
```js
<script setup>
const message = 'this is a message'
const logMessage = () =>{console.log(message)}
</script>
```
## reactive()和ref()

### reactive()
接受对象，返回响应式对象。  
要注意：reactive接受的一定是js对象！{a : 1}这种
```js
<script setup>
import {reactive } from 'vue'

const state = reactive({
  count : 0
})

const setCount = () =>{
  state.count++
}
</script>

<template>
  <div>
    <button @click="setCount">{{ state.count }}</button>
  </div>
</template>
```
### ref()
ref和reactive基本相似，但可以用于基础类型或者对象（更为通用）
ref()返回的是一个对象响应式对象，在script中访问需要.value！！  
相比于reactive，社区推荐使用ref！！
```js
<script setup>
import { ref } from 'vue'

const state = ref({
  count : 0
})

const setCount = () =>{
  state.value.count++//注意这个.value
}
</script>

<template>
  <div>
    <button @click="setCount">{{ state.count }}</button>//模板中访问不需要.value
  </div>
</template> 
```
