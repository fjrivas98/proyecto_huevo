<template>
  <div class="content" v-if="user != null">
    <input type="text" placeholder="nuevo usuario" v-model="db_user" id="user-input" name="user">
    <input type="password" placeholder="contraseña"  v-model="db_password" id="password-input" name="password">

    <button  @click="createUser()">Crear Usuario</button>


    <div id='example-3' class="container-check">
        <br>
        <label class="b-contain">
            <span>Seleccionar todos</span>
            <input type="checkbox" id="allcheck"  @click="selectAllCheck()">
            <div class="b-input"></div>
            </label>
        <div>
            <h4>Datos</h4>
            <label class="b-contain">
            <span>Select</span>
            <input class="group_form" type="checkbox" id="select" value="select" v-model="checkedNames">
            <div class="b-input"></div>
            </label>

            <label class="b-contain">
            <span>Insert</span>
            <input  class="group_form" type="checkbox" id="insert" value="insert" v-model="checkedNames">
            <div class="b-input"></div>
            </label>

            <label class="b-contain">
            <span>Update</span>
            <input  class="group_form" type="checkbox" id="update" value="update" v-model="checkedNames">
            <div class="b-input"></div>
            </label>


            <label class="b-contain">
            <span>Delete</span>
            <input  class="group_form" type="checkbox" id="delete" value="delete" v-model="checkedNames">
            <div class="b-input"></div>
            </label>


            <label class="b-contain">
            <span>File</span>
            <input  class="group_form" type="checkbox" id="file" value="file" v-model="checkedNames">
            <div class="b-input"></div>
            </label>
        </div>
        <div class="estructure">
            <h4>Estructura</h4>
            <label class="b-contain">
            <span>Create</span>
            <input class="group_form" type="checkbox" id="create" value="Create" v-model="checkedNames">
            <div class="b-input"></div>
            </label>

            <label class="b-contain">
            <span>alter</span>
            <input class="group_form" type="checkbox" id="alter" value="alter" v-model="checkedNames">
            <div class="b-input"></div>
            </label>

            <label class="b-contain">
            <span>index</span>
            <input class="group_form" type="checkbox" id="index" value="index" v-model="checkedNames">
            <div class="b-input"></div>
            </label>


            <label class="b-contain">
            <span>drop</span>
            <input class="group_form" type="checkbox" id="drop" value="drop" v-model="checkedNames">
            <div class="b-input"></div>
            </label>


            <label class="b-contain">
            <span>create temporary tables</span>
            <input class="group_form" type="checkbox" id="create_temp" value="create temporary tables" v-model="checkedNames">
            <div class="b-input"></div>
            </label>

            <label class="b-contain">
            <span>show view</span>
            <input class="group_form" type="checkbox" id="show_view" value="show view" v-model="checkedNames">
            <div class="b-input"></div>
            </label>

            <label class="b-contain">
            <span>create routine</span>
            <input class="group_form" type="checkbox" id="create_routine" value="create routine" v-model="checkedNames">
            <div class="b-input"></div>
            </label>

            <label class="b-contain">
            <span>alter routine</span>
            <input class="group_form" type="checkbox" id="alter routine" value="alter routine" v-model="checkedNames">
            <div class="b-input"></div>
            </label>

            <label class="b-contain">
            <span>execute</span>
            <input class="group_form" type="checkbox" id="execute" value="execute" v-model="checkedNames">
            <div class="b-input"></div>
            </label>

            <label class="b-contain">
            <span>create view</span>
            <input class="group_form" type="checkbox" id="create_view" value="create view" v-model="checkedNames">
            <div class="b-input"></div>
            </label>

            <label class="b-contain">
            <span>event</span>
            <input class="group_form" type="checkbox" id="event" value="event" v-model="checkedNames">
            <div class="b-input"></div>
            </label>

            <label class="b-contain">
            <span>trigger</span>
            <input class="group_form" type="checkbox" id="trigger" value="trigger" v-model="checkedNames">
            <div class="b-input"></div>
            </label>
        </div>
        
<div class="admin">
            <h4>Administracion</h4>
            <label class="b-contain">
            <span>Super</span>
            <input class="group_form" type="checkbox" id="super" value="super" v-model="checkedNames">
            <div class="b-input"></div>
            </label>

            <label class="b-contain">
            <span>Process</span>
            <input class="group_form" type="checkbox" id="process" value="process" v-model="checkedNames">
            <div class="b-input"></div>
            </label>

            <label class="b-contain">
            <span>Reload</span>
            <input class="group_form" type="checkbox" id="reload" value="reload" v-model="checkedNames">
            <div class="b-input"></div>
            </label>


            <label class="b-contain">
            <span>Shutdown</span>
            <input class="group_form" type="checkbox" id="shutdown" value="shutdown" v-model="checkedNames">
            <div class="b-input"></div>
            </label>


            <label class="b-contain">
            <span>show databases</span>
            <input class="group_form" type="checkbox" id="show_db" value="show databases" v-model="checkedNames">
            <div class="b-input"></div>
            </label>

            <label class="b-contain">
            <span>lock tables</span>
            <input class="group_form" type="checkbox" id="lock_tables" value="lock tables" v-model="checkedNames">
            <div class="b-input"></div>
            </label>

            <label class="b-contain">
            <span>references</span>
            <input class="group_form" type="checkbox" id="references" value="references" v-model="checkedNames">
            <div class="b-input"></div>
            </label>

            <label class="b-contain">
            <span>replication client</span>
            <input class="group_form" type="checkbox" id="replic_client" value="replication client" v-model="checkedNames">
            <div class="b-input"></div>
            </label>

            <label class="b-contain">
            <span>replication slave</span>
            <input class="group_form" type="checkbox" id="replic_slave" value="replication slave" v-model="checkedNames">
            <div class="b-input"></div>
            </label>

            <label class="b-contain">
            <span>create user</span>
            <input class="group_form" type="checkbox" id="create_user" value="create user" v-model="checkedNames">
            <div class="b-input"></div>
            </label>
        </div>

        <!-- <input type="checkbox" id="select" value="select" v-model="checkedNames">
        <label for="select">select</label>
        <input type="checkbox" id="insert" value="insert" v-model="checkedNames">
        <label for="insert">insert</label>
        <input type="checkbox" id="update" value="update" v-model="checkedNames">
        <label for="update">update</label>
         <input type="checkbox" id="delete" value="delete" v-model="checkedNames">
        <label for="mike">delete</label>
         <input type="checkbox" id="file" value="file" v-model="checkedNames">
        <label for="mike">file</label> -->
        
    </div>
    <div
        class="md-layout-item md-medium-size-100 md-xsmall-size-100 md-size-100"
      >
        <md-card>
          <md-card-header data-background-color="green">
            <h4 class="title">Usuarios</h4>
            <p class="category">Aquí puedes eliminar usuarios</p>
          </md-card-header>
          <md-card-content>
             <div>
              <md-table >
                <md-table-row :key=key v-for="(item, key) in user"  slot="md-table-row" >
                  <md-table-cell md-label="Name">{{item}}</md-table-cell>
                  <md-table-cell md-label="Delete"><md-button @click="deleteUser(item)" class="red-btn">Borrar</md-button></md-table-cell>
                   <md-table-cell md-label="Show"><button @click="showDb(item)">Visualizar</button></md-table-cell>
                </md-table-row>
              </md-table>
            </div>
          </md-card-content>
        </md-card>
      </div>
  </div>
</template>
<style>

input{
     padding: 5px;
     font-size: 16px;
     border-width: 1px;
     border-color: #CCCCCC;
     background-color: #FFFFFF;
     color: #000000;
     border-style: solid;
     border-radius: 0px;
     box-shadow: 0px 0px 5px rgba(66,66,66,.75);
     /* text-shadow: 0px 0px 5px rgba(66,66,66,.75); */
     margin-right: 8px;
     margin-bottom: 8px;
}
input:focus{
     outline:none;
}

button{
color: #20bf6b !important;
text-transform: uppercase;
background: #ffffff;
padding: 15px;
border: 4px solid #20bf6b !important;
border-radius: 6px;
display: inline-block;
transition: all 0.3s ease 0s;
}
button:hover {
color: #494949 !important;
border-radius: 50px;
border-color: #494949 !important;
transition: all 0.3s ease 0s;
}



.estructure{
    margin-left: 15px;
}
.container-check{
    display: flex;
    justify-content: flex-start;
    margin-bottom: 8px;
}
.b-contain *, .b-contain *::before, .b-contain *::after {
	box-sizing: content-box !important;
}

.b-contain input {
	position: absolute;
	z-index: -1;
	opacity: 0;
}

.b-contain span {
	line-height: 1.54;
	font-size: 1rem;
	font-family: inherit;
}

.b-contain {
	display: table;
	position: relative;
	padding-left: 1.8rem;
	cursor: pointer;
	margin-bottom: .5rem;
}

.b-contain input[type="checkbox"] ~ .b-input {
	position: absolute;
	top: 0;
	left: 0;
	height: 1.25rem;
	width: 1.25rem;
	background: rgba(241, 245, 248, 1);
	transition: background 250ms;
	border: 1px solid rgba(184, 194, 204, 1);
	border-radius: 0.125rem;
}

.b-contain input[type="radio"] ~ .b-input {
	position: absolute;
	top: 0;
	left: 0;
	height: 1.25rem;
	width: 1.25rem;
	background: rgba(241, 245, 248, 1);
	transition: background 250ms;
	border: 1px solid rgba(184, 194, 204, 1);
	border-radius: 2.0rem;
}

.b-contain input[type="checkbox"] ~ .b-input::after {
	content: '';
	position: absolute;
	display: none;
	left: .45rem;
	top: .18rem;
	width: .25rem;
	height: .6rem;
	border: solid rgba(255, 255, 255, 1);
	border-width: 0 2px 2px 0;
	transition: background 250ms;
	transform: rotate(45deg);
}

.b-contain input[type="radio"] ~ .b-input::after {
	content: '';
	position: absolute;
	display: none;
	left: .25rem;
	top: .25rem;
	width: .75rem;
	height: .75rem;
	border-radius: 2.0rem;
	background: rgba(255, 255, 255, 1);
	transition: background 250ms;
}

.b-contain input:disabled ~ .b-input::after {
	border-color: rgba(135, 149, 161, 1);
}

.b-contain input:checked ~ .b-input::after {
	display: block;
}

.b-contain:hover input ~ .b-input,
.b-contain input:focus ~ .b-input {
	background: rgb(231, 238, 243);
}

.b-contain input:focus ~ .b-input {
	box-shadow: 0 0 0 2px rgba(52,144,220,0.5);
}

.b-contain input:checked ~ .b-input {
	background: rgba(0, 130, 243, 1);
	border-color: rgba(0, 130, 243, 1);
}

.b-contain input[type="checkbox"]:disabled ~ .b-input {
	background: rgba(241, 245, 248, 1);
	border-color: rgba(184, 194, 204, 1);
	opacity: 0.6;
	cursor: not-allowed;
}

.b-contain input[type="radio"]:disabled ~ .b-input {
	background: rgba(241, 245, 248, 1);
	border-color: rgba(184, 194, 204, 1);
	opacity: 0.6;
	cursor: not-allowed;
}

.b-contain input[type="radio"]:disabled ~ .b-input::after {
	background: rgba(135, 149, 161, 1);
}

.b-contain input:checked:focus ~ .b-input, .b-contain:hover input:not([disabled]):checked ~ .b-input {
	background: rgba(13, 143, 255, 1);
	border-color: rgba(13, 143, 255, 1);
}

.b-contain .b-input::before {
	content: '';
	display: block;
	position: absolute;
	left: 0;
	top: 0;
	width: 3rem;
	height: 3rem;
	margin-left: -0.85rem;
	margin-top: -0.85rem;
	background: rgba(0, 130, 243, 1);
	border-radius: 2rem;
	opacity: .6;
	z-index: 99999;
	transform: scale(0);
}

@keyframes b-ripple {
	0% {
		transform: scale(0);
	}

	20% {
		transform: scale(1);
	}

	100% {
		opacity: 0;
		transform: scale(1);
  	}
}

@keyframes b-ripple-duplicate {
	0% {
		transform: scale(0);
	}

	30% {
		transform: scale(1);
	}

	60% {
		transform: scale(1);
	}

	100% {
		opacity: 0;
		transform: scale(1);
  	}
}

.b-contain input + .b-input::before {
	animation: b-ripple 250ms ease-out;
}

.b-contain input:checked + .b-input::before {
	animation-name: b-ripple-duplicate;
}

.b-contain .b-input::before {
	visibility: hidden;
}

.b-contain input:focus + .b-input::before {
	visibility: visible;
}

.b-contain:first-child .b-input::before {
	visibility: hidden;
}
</style>
<script>
const $ = require('jquery')

import Swal from 'sweetalert2'

export default {
  
  components: {

  },
  methods:{
    selectAllCheck(){
        this.checkedNames = [];
        var checks = document.getElementsByClassName("group_form");
        if(document.getElementById("allcheck").checked == true){
            for(let i = 0; i< checks.length; i++){
                checks[i].checked = true;
                this.checkedNames.push(checks[i].value);
            }
        }else{
            for(let i = 0; i< checks.length; i++){
                checks[i].checked = false;
            }
        }       
        
    },
    refreshData(){
      var that = this;
      $.ajax({
            url: "http://localhost/proyecto/proyecto/public/list_user.php",
            type: 'get',
            dataType: "json",
            success: function (data) {
                that.user = data;
            },
            error: function (jqXHR, textStatus, error) {
              console.error(error)
            }
      });
    },
    deleteUser(user){
      var that = this;
      var obj={
        "option":'delete',
        "db_user":user,
      }
        $.ajax({
          url: "http://localhost/proyecto/proyecto/public/list_user.php",
          type: 'post',
          data:obj,
          success: function (data) {
            if(data == true){
              that.refreshData();
              Swal.fire(
              'Enhorabuena!',
              'Usuario eliminada con éxito',
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
    createUser(){
        var that = this;
        if(that.checkedNames.length > 0){
            var obj={
              "option":"create",
              "db_user":that.db_user,
              "db_password":that.db_user,
              "db_permissions":that.checkedNames,
            }
        $.ajax({
          url: "http://localhost/proyecto/proyecto/public/list_user.php",
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
        }else{
            Swal.fire(
              'Atención!',
              'Debes de seleccionar al menos un permiso',
              'warning'
              )
        }
    }
  },
  beforeMount(){
    //por el puto contexto
    this.refreshData();
  },
  data() {
    return {
      value_input:"",
      user:null,
      db_user:"",
      db_password:"",
      checkedNames:[]
    };
  }
};
</script>
