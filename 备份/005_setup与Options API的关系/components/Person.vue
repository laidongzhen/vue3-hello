<template>
  <div class="person">
    <h2>姓名：{{name}}</h2>
    <h2>年龄：{{age}}</h2>
    <button @click="changeName">修改名字</button>
    <button @click="changeAge">修改年龄</button>
    <button @click="showTel">查看联系方式</button>
    <hr>
    <h2>测试1：{{a}}</h2>
    <h2>测试2：{{c}}</h2>
    <h2>测试3：{{d}}</h2>
    <button @click="b">测试</button>
  </div>
</template>
<!--
setup 与 Options API 的关系

- Vue2 的配置（`data`、`methods`......）中可以访问到 `setup`中的属性、方法。
- 但在`setup`中不能访问到`Vue2`的配置（`data`、`methods`......）。
- 如果与`Vue2`冲突，则`setup`优先。
 -->
<script lang="ts">
  export default {
    name:'Person',
    beforeCreate(){
      console.log('beforeCreate')
    },
    data(){
      return {
        a:100,
        c:this.name,
        d:900,
        age:90
      }
    },
    methods:{
      b(){
        console.log('b')
      }
    },
    setup(){
      // 数据，原来是写在data中的，此时的name、age、tel都不是响应式的数据
      let name = '张三'
      let age = 18
      let tel = '13888888888'

      // 方法
      function changeName() {
        name = 'zhang-san' //注意：这样修改name，页面是没有变化的
        console.log(name) //name确实改了，但name不是响应式的
      }
      function changeAge() {
        age += 1 //注意：这样修改age，页面是没有变化的
        console.log(age) //age确实改了，但age不是响应式的
      }
      function showTel() {
        alert(tel)
      }

      // 将数据、方法交出去，模板中才可以使用
      return {name,age,tel,changeName,changeAge,showTel}

      // setup的返回值也可以是一个渲染函数
      // return ()=>'哈哈'
    }
  }
</script>

<style scoped>
  .person {
    background-color: skyblue;
    box-shadow: 0 0 10px;
    border-radius: 10px;
    padding: 20px;
  }
  button {
    margin: 0 5px;
  }
</style>
