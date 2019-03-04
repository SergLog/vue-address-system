<template>
  <div id="app">
    <div class="header">
  <img src="/src/assets/logo.png" style="width: 80px">  
  <span>Адресная система отдела картографии УИТС г. Сургута</span>
</div > 
    <div class="navigation">
      <b-card no-body>
    <b-tabs pills card vertical content-class="mt-3">
      <b-tab title="Справочник городов" active>
        <base-list v-bind:items="citiesArray" v-bind:columns="columns"></base-list>
      </b-tab>
      <b-tab title="Справочник поселков">I'm the second tab content</b-tab>
      <b-tab title="Справочник улиц">Disabled tab!</b-tab>
  </b-tabs>
  </b-card>
   </div>
  </div>
</template>

<script>

import baseList from './components/baseList.vue'
import axios from 'axios'

export default {
  name: 'app',
  components: { baseList },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      // citiesArray: [
      //     {id: 1, name: 'Сургут'},
      //     {id: 2, name: 'Москва'},
      //     {id: 3, name: 'Ростов'},
      //     {id: 4, name: 'Пенза'},
      //     {id: 5, name: 'Ставрополь'},
      //     {id: 6, name: 'Нью-Йорк'},
      //],
      citiesArray: null,
      columns: [
        {name: 'id', width: '10%'},
        {name: 'Наименование', width: '70%'},
        {name: 'Действия', width: '20%'},

        ],
    }
  }, 
  created() {
    axios.get(`http://localhost:25535/api/streets`)
    .then(response => {
      
      this.citiesArray = response.data;
      
    })
    .catch(e => {
      //this.errors.push(e)
      console.log(e);
    })
  }    
  }
</script>

<style>
.header {
    text-align: center;
    margin-top: 10px;
    margin-bottom: 35px;
    /* background-color: #87CEEB; */
  }
  .navigation {
    margin-right : 50px;
    margin-left : 50px;
}
span {
    font-size: 35px;
    margin-left: 15px;
}
  .tab-pane:focus{ 
    outline: none;
}
</style>
