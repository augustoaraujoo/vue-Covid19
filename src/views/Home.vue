<template>
  <div>
    <p>home !</p>
    ir para<router-link to="/About">About</router-link>
    <p>Rest api</p>
    <header>
      <input type="text" v-model="filter" />
      <tbody class="infosAll">
        <tr v-for="todo in filterCountry" :key="todo">
          <td><img :src="todo.countryInfo.flag" /></td>
          <td>country : {{ todo.country }}</td>
          <td>cases : {{ todo.cases }}</td>
          <td>deaths : {{ todo.deaths }}</td>
          <td>today cases : {{ todo.todayCases }}</td>
          <td>today deaths : {{ todo.todayDeaths }}</td>
        </tr>
      </tbody>
    </header>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      todos: null,
      countryDigitada: null,
      filter: "",
    };
  },
  computed: {
    filterCountry() {
      if (!this.filter) return this.todos;
      return this.todos.filter((todos) =>
        todos.country.toLowerCase().includes(this.filter.toLowerCase())
      );
    },
  },
  mounted() {
    this.getApi();
  },
  methods: {
    async getApi() {
      try {
        axios.get(`https://corona.lmao.ninja/v2/countries`).then((response) => {
          this.todos = response.data;
          console.log(response);
        });
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
<style scoped>
img {
  width: 140px;
}
</style>
