<template>
  <div> 
    <p>home !</p>
    ir para<router-link to="/About">About</router-link>

    <header>
      <input type="text" v-model="getValueInput" @keyup="getApi">
      <button @click="getApi">clicar</button>
      <p id="res"></p>
      <ul  class="container">
        <li v-for="flag in flags" :key="flag" type="none">
          <img :src="flag">
        </li>
      </ul>
     </header>
  </div>
</template>

<script>
export default {
  data:()=>({
      getValueInput:'brasil',
      flags:null
  }),
  mounted(){
    this.getApi()
  },
  methods: {
    async getApi(){
      try{
        const req = await fetch(`https://corona.lmao.ninja/v2/countries/`)//
         const data = await req.json()
          const viewFlags = data.map((e)=>{
           return e.countryInfo.flag
          })
           this.flags = viewFlags
            console.log(data)
            
        /**/
          const re2 = await fetch(`https://corona.lmao.ninja/v2/countries/${this.getValueInput}`)
           const data2 = await re2.json()
            console.log(data2)

      }catch(err){
        console.log(err.message)
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