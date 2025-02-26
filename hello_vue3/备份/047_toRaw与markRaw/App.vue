<template>
  <div class="app">
    <h2>姓名：{{ person.name }}</h2>
    <h2>年龄：{{ person.age }}</h2>
    <button @click="person.age += 1">修改年龄</button>
    <hr>
    <h2>{{ car2 }}</h2>
    <button @click="car2.price += 10">点我价格+10</button>
  </div>
</template>

<script setup lang="ts" name="App">
  import { reactive,toRaw,markRaw } from "vue";
  import mockjs from 'mockjs'

  /* toRaw */
  let person = reactive({
    name:'tony',
    age:18
  })
  // 用于获取一个响应式对象的原始对象
  let rawPerson = toRaw(person)
  console.log('响应式对象',person)   //Proxy(Object) {name: 'tony', age: 18}
  console.log('原始对象',rawPerson)  //{name: 'tony', age: 18}


  /* markRaw */
  let car = markRaw({brand:'奔驰',price:100})
  let car2 = reactive(car)

  // 可以看到响应式对象不再生效
  console.log(car)   //{brand: '奔驰', price: 100, __v_skip: true}
  console.log(car2)  //{brand: '奔驰', price: 100, __v_skip: true}

  let mockJs = markRaw(mockjs)  //{Handler: {…}, Random: {…}, Util: {…}, RE: {…}, XHR: ƒ, …}
</script>

<style scoped>
	.app {
		background-color: #ddd;
		border-radius: 10px;
		box-shadow: 0 0 10px;
		padding: 10px;
	}
	button {
		margin:0 5px;
	}
</style>