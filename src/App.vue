<template>
  <div>
    <Addtask></Addtask>
    <div class="scr">
      <Task  v-for="i in tasks" :key="i.id">
        <button class="btn-3" :class="{green : i.completed }" @click="setcomplete(i.id)">completed</button>
        <h1 class="task-desc">{{i.task}}</h1>
        <div class="edit-box" v-if="i.edit">
          <input type="text" v-model="i.task" class="edit-bar">
          <button class="main-btn btn-2" @click="editinit(i.id)">Save</button>
        </div>
        <button v-if="!i.edit" class="main-btn" @click="editinit(i.id)">Edit</button>
        <button class="main-btn red-btn" @click="deleteinit(i.id)">Delete</button>
      </Task>
    </div>
  </div>
</template>

<script>
import { mybus } from './main';
import Addtask from './Components/addtask';
import Task from './Components/task';
export default {
  components:{
    Addtask : Addtask,
    Task : Task
  },
  data:function(){
    return{
      tasks:[]
    }
  },
  methods:{
    addit(obj){
      this.tasks.push(obj);
    },
    deleteinit(myid){
        this.tasks.map((b,c) => {
          if(b.id == myid){
            this.tasks.splice(c,1);
          }
        });
    },
    editinit(myid){
      console.log(myid);
      this.tasks.map((b,c) => {
          if(b.id == myid){
            b.edit = !b.edit;
          }
        });
    },
    setcomplete(myid){
      this.tasks.map((b,c) => {
          if(b.id == myid){
            b.completed = !b.completed;
          }
        });
    }
  },
  created(){
    mybus.$on("adding",(obj) => this.addit(obj))
  }
}
</script>

<style scoped>
    .main-btn{
      font-size: 1.3rem;
      outline: none;
      border: none;
      border-radius: 40rem;
      padding: .6rem;
      width: 100px;
      cursor: pointer;
    }
    .red-btn{
      background-color: tomato;
    }
    .scr{
      overflow: scroll;
    }
    .btn-2{
      background-color: green;
      font-size: 1rem;
      width: 80px;
    }
    .edit-box{
      display: block;
      margin: 1rem;
    }
    .edit-bar{
      width: 250px;
      border: none;
      outline: none;
      height: 2rem;
      border-radius: 50rem;
      padding-left: 1rem;
      background-color: lightsteelblue;
    }
    .green{
      background-color: green;
    }
    .red{
      background-color: red;
    }
    .btn-3{
      border-radius: 50rem;
      outline: none;
      font-size: 1.5rem;
      width: 15rem;
    }
</style>