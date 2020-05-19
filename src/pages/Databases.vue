<template>
  <div class="content" v-if="databases != null">
    <div v-if="all">
      <!-- <div :key=item v-for="item in databases">{{item}} <button @click="deleteDatabase(item)">Eliminar</button></div> -->
      <input type="text"  v-model="value_input" id="database-input" name="database">
      <button  @click="createDatabase()">Crear base de datos</button>
      <div
          class="md-layout-item md-medium-size-100 md-xsmall-size-100 md-size-100"
        >
        <md-card>
          <md-card-header data-background-color="green">
            <h4 class="title">Simple Table</h4>
            <p class="category">Here is a subtitle for this table</p>
          </md-card-header>
          <md-card-content>
             <div>
              <md-table >
                <md-table-row :key=item v-for="item in databases"  slot="md-table-row" >
                  <md-table-cell md-label="Name">{{item}}</md-table-cell>
                  <md-table-cell md-label="Delete"><md-button @click="deleteDatabase(item)" class="red-btn">Borrar</md-button></md-table-cell>
                   <md-table-cell md-label="Show"><button @click="show(item)">Visualizar</button></md-table-cell>
                </md-table-row>
              </md-table>
            </div>
          </md-card-content>
        </md-card>
      </div>
    </div>
    <div v-else>
      <databaseview
      :name="namedb"
      v-on:show="show($event)"
      >
      </databaseview>
    </div>
    
  </div>
</template>
<style>

</style>
<script>
const $ = require('jquery')

import Swal from 'sweetalert2'

import {Databaseview} from "@/components";

export default {
  
  components: {
    Databaseview
  },
  name:"papa",
  methods:{
    show(name){
      this.all = !this.all;
      this.namedb = name
    },
    refreshData(){
      var that = this;
      $.ajax({
            url: "http://localhost/proyecto/proyecto/public/prueba3.php",
            type: 'get',
            dataType: "json",
            success: function (data) {
                that.databases = data;
            },
            error: function (jqXHR, textStatus, error) {
              console.error(error)
            }
      });
    },
    deleteDatabase(db){
      var that = this;
      var obj={
        "option":'delete',
        "db_name":db,
      }
        $.ajax({
          url: "http://localhost/proyecto/proyecto/public/create_database.php",
          type: 'post',
          data:obj,
          success: function (data) {
            if(data == true){
              that.refreshData();
              Swal.fire(
              'Enhorabuena!',
              'Base de datos eliminada con éxito',
              'success'
              )
            }else{
              Swal.fire(
              'Error!',
              'Hubo un problema al crear la base de datos',
              'error'
              )
            }
          },
          error: function (jqXHR, textStatus, error) {
            console.error(error)
          }
        });
    },
    createDatabase(){
        var that = this;
            var obj={
              "option":"create",
              "db_name":that.value_input,
            }
        $.ajax({
          url: "http://localhost/proyecto/proyecto/public/create_database.php",
          type: 'post',
          data:obj,
          success: function (data) {
            if(data == true){
              that.refreshData();
              Swal.fire(
              'Enhorabuena!',
              'Base de datos creada con éxito',
              'success'
              )
            }else{
              Swal.fire(
              'Error!',
              'Hubo un problema al crear la base de datos',
              'error'
              )
            }
          },
          error: function (jqXHR, textStatus, error) {
            console.error(error)
          }
        });
    }
  },
  beforeMount(){
    //por el puto contexto
    this.refreshData();
  },
  data() {
    return {
      value_input:"",
      databases:null,
      namedb:"",
      all:true
    };
  }
};
</script>
