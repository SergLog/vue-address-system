<template>
 <div class="container mt-4">
      
      <b-row>
      <b-col md="7" class="my-1 mb-4">
        <b-form-group label-cols-sm="3" label="Поиск" class="mb-0">
          <b-input-group>
            <b-form-input v-model="searchName" placeholder="Введите текст для поиска"/>
            <b-input-group-append>
              <b-button :disabled="!searchName" @click="searchName = ''">Очистить</b-button>
            </b-input-group-append>
          </b-input-group>
        </b-form-group>
      </b-col> 
      <b-col>
         <b-button variant="outline-success" size="sm" v-show="editIndex !== 0 && !editIndex" @click="add">Добавить новую запись</b-button>
      </b-col>    
    </b-row>     

    <b-row>       
    <table class="table table-bordered table-sm">
      <thead class="thead-light text-center">
        <tr>
          <th v-for="(item, index) in columns" :key="index" v-bind:width="item.width"> {{ item.name }} </th>
        </tr>
      </thead>
      <tbody>
         
        <!-- <tr v-for="(item, index) in items" :key="index"> -->
        <tr v-for="(item, index) in items" :key="index" v-show="filterName(item.адрес, item.isNew)">
          <!-- <td>{{ item }}</td> -->
          <td class="align-middle">
            <span v-if="editIndex !== index"> {{ item.код }} </span>
            <span v-if="editIndex === index">
              <b-form-input class="bg-light" v-model="item.код"></b-form-input>
            </span>           
          </td>
          <td>
            <span v-if="editIndex !== index"> {{ item.адрес }} </span>
            <span v-if="editIndex === index">
              <b-form-input class="bg-light" v-model="item.адрес"></b-form-input>
            </span>    
          </td>
          <td class="align-middle">
            <span v-if="editIndex !== index">
              <b-button variant="outline-secondary" size="sm" @click="edit(item, index)">Редактировать</b-button>
              <b-button variant="outline-danger" size="sm" @click="remove(item, index)">Удалить</b-button>
            </span>
            <span v-else>
              <b-button variant="outline-dark" size="sm" @click="cancel(item)">Отмена</b-button>
              <b-button variant="outline-success" size="sm" @click="save(item)">Сохранить</b-button>
            </span>
          </td>
        </tr>
      </tbody>
    </table>
    </b-row>
        <!-- <div class="col-3 offset-9 text-right my-3"> -->
      <b-button variant="outline-success" size="sm" v-show="editIndex !== 0 && !editIndex" @click="add">Добавить новую запись</b-button>
    <!-- </div> -->

  </div>
</template>

<script>

import axios from 'axios'

export default {
//   name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      editIndex: null,
      isAdd: false,
      searchName: ""
    }
  },
  props: {
    columns: null,
    items: null
  },
  methods: {  

     add() {      
      this.items.push({ код: '', адрес: '', isNew: true});
      this.editIndex = this.items.length - 1;
      this.isAdd = true;
      this.searchName = "Идет добавление новой записи...";
    },

    сlearSearch() {
      this.searchName = '';

    },
    edit(item, index) {
      this.editIndex = index;
    },

    cancel(item) {
      this.editIndex = null ;
      if (this.isAdd) {
      this.items.splice(this.items.indexOf(item), 1);
      this.isAdd = false;
      this.searchName = '';
      this.isNew = false;
      }
    },

    remove(item, index) {
      this.items.splice(index, 1);
    },

    save(item) {
      this.editIndex = null;
      if (item.isNew) {
        alert('Запись добавлена!')
      }
      else{
        alert('Запись сохранена!')
      }
      item.isNew = false;
      this.searchName = '';
      

    },
    filterName(itemname, isnew) {

        if (itemname.toLowerCase().includes(this.searchName.toLowerCase()) || isnew) {      
        return true;
      }       
       return false;
    },
  },
}
</script>

<style scoped>
span {
    font-size: 15px;
  }
.table .thead-light th {
  color: white;
  background-color: #007bff;
  border-color: #dee2e6;
}
</style>
