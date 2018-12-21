<template>
  <div id="app">
    <div class="inp">
      <p>ToDoList</p>
      <input type="text" v-model="todo" @keydown="getadd($event)" placeholder="添加ToDo">
    </div>
    <!-- <button @click="getadd()">点击</button> -->
    <div class="bot"> 
      <p class="word">正在进行</p>
      <ul v-for="(item,index) in list" v-if="!item.checked">
        <li>
          <p>
            <input type="checkbox" v-model="item.checked" id="ii1">
            <label for="ii1">{{item.title}}</label>
          </p>
          <button @click="removein(index)">删除</button>
        </li>
      </ul>
      <p class="word">已经完成</p>
      <ul v-for="(item,index) in list" v-if="item.checked">
        <li>
          <p>
            <input type="checkbox" v-model="item.checked" id="ii2">
            <label for="ii2">{{item.title}}</label>
          </p>
          <button @click="removein(index)">删除</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      todo:'',
      list:[
        {
          title:"正在进行中：",
          checked:false
        },
        {
          title:"已完成：",
          checked:true
        }
      ]
    }
  },
  methods:{
    getadd(e){
      console.log(e.keyCode)
      // this.list.push(this.todo)
      // this.todo = ''
      if(e.keyCode==13){
        this.list.push({
          title:this.todo,
          checked:false
        })
        this.todo = ''
      }
      localStorage.setItem('list',JSON.stringify(this.list))
    },
    removein(index){
      this.list.splice(index,1)
      localStorage.setItem('list',JSON.stringify(this.list))
    }
  },
  mounted(){
    var list = JSON.parse(loaclStorage.getItem('list'));
    if(list){
      this.list = list
    }
  }
}
</script>

<style>
  *{
    margin: 0;
    padding: 0;
    list-style: none;
  }
  .inp{
    width: 100%;
    height: 60px;
    background: #1E1E1E;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .inp p{
    font-size: 40px;
    color: #eee;
    margin: 0 0 0 350px;
  }
  .inp input{
    width: 250px;
    height: 38px;
    margin: 0 auto; 
    text-indent: 10px;
    background: #eee;
    border: 1px solid pink;
    border-radius: 8px;
  }
  .bot{
    width: 100%;
  }
  .word{
    width: 100%;
    height: 100px;
    padding: 0 150px;
    line-height: 100px;
    box-sizing: border-box;
    font-size: 30px;
    font-weight: bold;
  }
  .bot li{
    width: 67%;
    height: 50px;
    margin: 10px auto;
    border-radius: 8px;
    background: linear-gradient(to right,#007ACC 0.2%,#eee 3%);
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .bot li p{
    margin: 0 50px;
    font-size: 16px; 
    color: darkslategray;
  }
  .bot li p input{
    margin: 0 5px;
  }
  .bot li button{
    width: 80px;
    height: 35px;
    margin: 0 50px;
    font-size: 13px;
    color: tomato;
    border: 1px solid tomato;
    background: #fff;
    border-radius: 8px;
  }
</style>
