<template>
  <div id="app">
    <div class="header">
  <img src="/src/assets/logo.png" style="width: 80px">  
  <span>Адресная система отдела картографии УИТС г. Сургута</span>
</div > 
    <div class="navigation">
    <b-tabs content-class="mt-3">
      <b-tab title="Справочник городов" active>I'm the first fading tab</b-tab>
      <b-tab title="Справочник поселков">I'm the second tab content</b-tab>
      <b-tab title="Справочник улиц">Disabled tab!</b-tab>
  </b-tabs>
   </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
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
</style>
