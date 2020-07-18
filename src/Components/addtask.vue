<template>
  <div class="input-box">
    <input type="text" class="input-bar" v-model="newtask.task" @keypress.enter="addinginit" />
    <button @click="addinginit" class="input-button">ADD</button>
  </div>
</template>

<script>
import { mybus } from '../main';
export default {
  data:function(){
      return{
          newtask :{
              task : "",
              id : "",
              completed : false,
              edit : false,
          }
      }
  },
  methods:{
      addinginit(){
          this.newtask.id = this.newtask.task;
          var temp = {...this.newtask}
          mybus.$emit("adding",temp);
          this.newtask.task = "";  
      }
  }
}
</script>

<style scoped>
    .input-box{
        widows: 100vw;
        padding: 1rem;
        text-align: center;
        background-color: thistle;
    }
  .input-bar{
    width: 70vw;
    /* border: none; */
    outline: none;
    font-size: 2rem;
    height: 3rem;
    padding-left: .5rem;
    padding-right: .5rem;
    overflow: scroll;
  }
  .input-button{
      font-size: 1.6rem;
      padding: .6rem;
  }
</style>