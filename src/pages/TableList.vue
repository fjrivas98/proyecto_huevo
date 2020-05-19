<template>
  <div class="content">
    <button  @click="createBackup()">Crear Copia de Seguridad de la Base de datos</button>
  </div>
</template>

<script>
const $ = require('jquery')
import Swal from 'sweetalert2'
import { SimpleTable, OrderedTable ,Databaseview} from "@/components";

export default {
  methods:{
    createBackup(){
      
        var that = this;
            var obj={
            }
        $.ajax({
          url: "http://localhost/proyecto/proyecto/public/create_backup.php",
          type: 'post',
          data:obj,
          success: function (data) {
            if(data == true){
              Swal.fire(
              'Enhorabuena!',
              'Volcado de la Base de Datos realizada con éxito!',
              'success'
              )
            }else{
              Swal.fire(
              'Error!',
              'Hubo un problema al crear la copia de seguridad',
              'error'
              )
            }
          },
          error: function (jqXHR, textStatus, error) {
            console.error(error)
          }
        });
    }
  }



};

</script>
