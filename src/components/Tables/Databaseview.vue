<style scoped>
  .p-empty{
    position: absolute;
    left: 25%;
    top: 50%;
    font-size: 2.5rem;
  }
  .cotainer-h2{
    display: flex;
    justify-content: space-between;
    border-bottom: 1px solid grey;

  }

  .dis-flex{
    display: flex;
    flex-wrap: wrap;
    justify-content: flex-start;
  }
  .container-h3{
    max-width: 325px;
    width: auto;
    min-width: 100px;
  }
  /* .ellipsis-text{
        white-space: nowrap;
        text-overflow: ellipsis;
        display: flex;
        align-items: center;
        cursor: pointer;
        overflow: hidden;
        width: calc(100% - 10px);
    } */
  h3{
     margin: 10px 0;
     max-width: 370px;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    }
  button{
    margin: 2px 5px;
  }
  .card{
    width: 390px;
    margin: 5px;
    padding:5px 10px;
    display: flex;
    flex-direction: column;
    background-color: white;
  }
  .container-button{
    display: flex;
    justify-content: flex-end;
  }
</style>
<template>
<div>
  <div v-if="identifier == 'show_tables'">
    <button @click="changeView('create_table')">crear tablas</button>
    <div class="cotainer-h2">
        <h2 class="title">{{name}}</h2>
        <button style="display:iline-block" @click="$emit('show')">Volver</button>
      </div>

      <div class="dis-flex" v-if="tables.length > 0"> 
        <div class="card" :key=item v-for="item in tables">
          <div class="ellipsis-text"> <h3 :title=item>{{item}}</h3></div>
          <div class="container-button">
            <button  @click="createDatabase()">Modificar</button>
            <button  @click="deleteTable(item)">Eliminar</button>
          </div>
        </div>
      </div>
      <div v-else class="container-empty">
        <p class="p-empty">Esta base de datos no contiene ninguna tabla</p>
  </div>

  </div>
  

  <div v-if="identifier == 'create_table'">
    <button @click="changeView('show_tables')">volver a listado de tablas</button>
    <input type="text" placeholder="nombre de la nueva tabla" v-model="new_table" class="all_inputs">
    <div id="container-input" :key=index v-for="(item, index) in group_inputs">
        <input type="text"  v-model="item.name" class="all_inputs">
       <select v-model="item.type">
        <option disabled value="">Seleccione un elemento</option>
        <option>int</option>
        <option>text</option>
        <option>varchar</option>
        <option>date</option>
      </select>
      <input v-if="group_inputs[index].type == 'int' ||  group_inputs[index].type == 'varchar'" type="number" v-model="item.number" class="all_inputs">
      <input v-if="group_inputs[index].type == 'date' " type="date" v-model="item.number" class="all_inputs">
    </div>
    <button @click="addField()">añadir campo</button>
    <button @click="createTable()">crear tabla</button>
  </div>
 
  <!-- <div class="content" v-if="databases != null"> -->
    <!-- <div :key=item v-for="item in databases">{{item}} <button @click="deleteDatabase(item)">Eliminar</button></div>
    <input type="text"  v-model="value_input" id="database-input" name="database">
    <button  @click="createDatabase()">Create database</button>
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
                  <md-table-cell md-label="Delete"><md-button @click="deleteDatabase(item)" class="red-btn">delete</md-button></md-table-cell>
                   <md-table-cell md-label="Show"><button @click="showDb(item)">Visualizar</button></md-table-cell>
                </md-table-row>
              </md-table>
            </div>
          </md-card-content>
        </md-card>
      </div> -->
  </div>
</template>
<script>
const $ = require('jquery')

import Swal from 'sweetalert2'

export default {
  
  components: {

  },
  props: {
    name:String
  },
  methods:{
    refreshData(){
      var that = this;
      $.ajax({
            url: "http://localhost/proyecto/proyecto/public/create_tables.php?name="+that.name,
            type: 'get',
            dataType: "json",
            success: function (data) {
                that.tables = data;
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
    },
    createTable(){
        var that = this;
            var obj={
              "option":"create_table",
              "db_name":this.name,
              "table_name":this.new_table,
              "params":this.group_inputs
            }
        $.ajax({
          url: "http://localhost/proyecto/proyecto/public/create_database.php",
          type: 'post',
          data:obj,
          success: function (data) {
            if(data == true){
              that.identifier = "show_tables";
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
    },
    deleteTable(table){
      var that = this;
      var obj={
        "option":'deletetable',
        "db_name":this.name,
        "table_name":table,
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
              'Columna eliminada con éxito',
              'success'
              )
            }else{
              Swal.fire(
              'Error!',
              'Hubo un problema al',
              'error'
              )
            }
          },
          error: function (jqXHR, textStatus, error) {
            console.error(error)
          }
        });
    },
    changeView(identifier){
      this.new_table = "";
      this.group_inputs =  [
        {name:"",type:"",number:0,}
      ];
      this.identifier = identifier;
    },
    addField(){
      this.group_inputs.push({name:"",type:"",number:0,})
    }
  },
  beforeMount(){
    //por el puto contexto
    this.refreshData();
  },
  data() {
    return {
      value_input:"",
      tables:[],
      identifier:'show_tables',
      all_values:{},
      new_table:"",
      group_inputs:[
        {name:"",type:"",number:0,}
      ]
    };
  }
};
</script>
