<script>
  import ChildComponent from './ChildComponent.vue'

  export default{
    data(){
      return {
        message: "test",
        count: 0,
        input1:"",
        ifTest:true,
        someList : [
          {id:1, data:"yeah"},
          {id:2, data:"yeah 2"},
          {id:3, data:"yeah 3"}
        ],
        onlyFirstSomeList: false,
        msgToChild:"Child works",
        childMsg:'No Child msg'
      }
    }, 
    mounted(){
      this.$refs.p.textContent = "bye"
    },
    components:{
      ChildComponent
    },
    computed:{
      updateSomeList(){
        return this.onlyFirstSomeList ? 
        this.someList.filter((f)=>f.id==1) :
        this.someList
      }
    },
    watch:{
      onlyFirstSomeList(){
        console.log("Triggers");
      }
    },
    methods:{
      increment(){
        this.count++;
      },

      inputData(e){
        this.input1 = e.target.value;
      }

    }
  }
</script>

<template>
  <h1>{{ message }}</h1>
  <div v-bind:id="divId"></div>

  <input v-bind:value="input1" v-on:input="inputData" />
  <input v-model="input1"/>
  <p>{{ input1 }}</p>

  <button v-on:click="increment">Count is : {{ count }}</button>

  <h1 v-if="ifTest">Vue rocks!!!</h1>

  <ul>
    <li v-for="i in someList" v-bind:key="i.id">{{ i.data }}</li>
  </ul>

  <button v-on:click="onlyFirstSomeList = !onlyFirstSomeList">
    {{ !onlyFirstSomeList ? "Show only first" : "Show all" }} </button>
  <ul>
    <li v-for="i in updateSomeList" v-bind:key="i.id">{{ i.data }}</li>
  </ul>

  <p ref="p">Good</p>

  <ChildComponent v-bind:msg="msgToChild"/>
  
  <ChildComponent v-on:response="(msg) => childMsg = msg"/>
  <p>{{ childMsg }}</p>

  <ChildComponent>Message : {{childMsg}}</ChildComponent>
</template>