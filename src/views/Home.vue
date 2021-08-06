<template>
  <div> 
    <p>home !</p>
    ir para<router-link to="/About">About</router-link>

  <header>
  <input type="text">
    <ul>
      <li v-for="todo in todos " :key="todo">
      {{todo.country}}
      <img :src="todo.countryInfo.flag">
      cases: {{todo.cases}}
      </li>
    </ul>
  </header>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      todos:null,
      countryDigitada:null
    }
  },
  mounted(){
    this.getApi();
  },
  methods: {
   async getApi(){
     try{
       axios
          .get(`https://corona.lmao.ninja/v2/countries`)
            .then(response =>{
              this.todos = response.data
              console.log(response);
        })
     }catch(error){
        console.log(error)
     }
      
    }
  },
}
</script>
<style scoped>
.container{
  display: flex;
  justify-content: space-between;
  flex-direction: row;
  flex-wrap: wrap;
  height: 100vh;
  margin: auto;
}
img:hover{
  transform: scale(1.1);
  transition: .3s;
}
img{
  width: 150px;
}
</style>