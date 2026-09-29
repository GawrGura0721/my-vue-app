<script setup>
import { ref } from 'vue'
import axios from 'axios';

getlist()

const value=ref('')

const list=ref([

  
])

async function add(){
  await axios({
    url:"https://ssng0yo65y.sealoshzh.site/add_todo",
    method:"POST",
    data:{
      value:value.value,
      isCompleted:false
    }
  })
  getlist()

  value.value=''
}

async function del(id){
  await axios({
      url:"https://ssng0yo65y.sealoshzh.site/del_todo",
      method:"POST",
      data:{
        id
      }
  })

  getlist()
}

async function getlist(){
  const res =await axios({
    url:"https://ssng0yo65y.sealoshzh.site/get_list",
    method:"GET"
  })

  list.value=res.data.list
  console.log(res);
  
}

async function update(id){
  await axios({
    url:"https://ssng0yo65y.sealoshzh.site/update_todo",
    method:"POST",
    data:{
      id
    }
  })

  getlist()
}


</script>
<template>
  <div class="todo-app">
    <div class="title">小鲨鱼牌便签</div>

    <!-- 输入框 -->
    <div class="todo-form">
      <input
        v-model="value"
        type="text"
        class="todo-input"
        placeholder="Add a todo"
      />
      <div @click="add" class="todo-button">Add Todo</div>
    </div>


    <!-- item -->
    <div v-for="(item,index) in list" :class="[item.isCompleted ? 'completed':'item']">
      <div>
        <input @click="update(item._id)"" v-model="item.isCompleted" type="checkbox" />
        <span class="name">{{ item.value }}</span>
      </div>

      <div @click="del(item._id)" class="del">del</div>
    </div>
  </div>
</template>

<style scoped>
.todo-app {
  box-sizing: border-box;
  margin-top: 40px;
  margin-left: 1%;
  padding-top: 30px;
  width: 98%;
  height: 500px;
  background: #ffffff;
  border-radius: 5px;
}

.title {
  text-align: center;
  font-size: 30px;
  font-weight: 700;
  user-select: none;
}

.todo-form {
  display: flex;
  margin: 20px 0 30px 20px;
}

.todo-button {
  width: 100px;
  height: 52px;
  border-radius: 0 20px 20px 0;

  text-align: center;
  background: linear-gradient(
    to right,
    rgb(113, 65, 168),
    rgba(44, 114, 251, 1)
  );
  color: #fff;
  line-height: 52px;
  cursor: pointer;
  font-size: 14px;
  user-select: none;
}

.todo-input {
  padding: 0px 15px 0px 15px;
  border-radius: 20px 0 0 20px;
  border: 1px solid #dfe1e5;
  outline: none;
  width: 60%;
  height: 50px;
}

.item {
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 80%;
  height: 50px;
  margin: 8px auto;
  padding: 16px;
  border-radius: 20px;
  box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 20px;
  user-select: none;
}

.del {
  color: red;
  cursor: pointer;
}

.completed {
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 80%;
  height: 50px;
  margin: 8px auto;
  padding: 16px;
  border-radius: 20px;
  box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 20px;
  text-decoration: line-through;
  opacity: 0.4;
  user-select: none;
}
</style>
