<template lang="html">
    
    <div class="contenedor">
      <v-layout  d-block>
        <div class="cabeceras">
            <h1>Crear clasificacion</h1>
        </div>

        <v-flex xs12 sm8 md6>
          
            <v-card class="form">
                <v-card-title class="headline">Crear Clasificación</v-card-title>

                  <v-text-field
                  class="clasificacion"
                  :counter="80"
                  maxlength="80"
                  :rules="clasificacionRules"
                  v-model="agregarClasificacion.clasificacion"
                  label="Nombre de la clasificación"
                  outline
                  required
                  ></v-text-field>
                  <br>
                  <br>
                  <br>
                  <br>

                  <v-textarea
                  class="textarea_descripcion"
                  outline
                  maxlength="200"
                  :counter="200"
                  v-model="agregarClasificacion.descripcion"
                  label="Descripcción"
                  required>
                  </v-textarea>
    

                  <v-btn class="input_button" @click="addClasificacion">Guardar</v-btn>
                  <v-btn class="input_button" v-on:click="clear">Limpiar</v-btn>
              </v-card>
            </v-flex>
      </v-layout>
    </div>
    
</template>

<script>

import Firebase from 'firebase';
import config from './config';

let app = Firebase.initializeApp(config);
let db = app.database();
let agregarClasificacion = db.ref('clasificacion');

export default {
  
  firebase: {
    clasificacion: agregarClasificacion
  },

  data() {
    return {
      agregarClasificacion: {
        clasificacion: '',
        descripcion: ''
      },
      clasificacionRules: [v => !!v || 'Este campo es requerido']
    }
  },

  methods: {
    clear() {
      this.agregarClasificacion.clasificacion = ''
      this.agregarClasificacion.descripcion = ''
      //Toastr.error('fffff')
    },
    addClasificacion() { 
      if (this.agregarClasificacion.clasificacion == '' ||  this.agregarClasificacion.descripcion == ''){
          //Toastr.error('Hay algun campo repetido ó vacio')
          console.log("Hay un campo vacio")
      } else{
        agregarClasificacion.push(this.agregarClasificacion); 
        this.agregarClasificacion.clasificacion = ''
        this.agregarClasificacion.descripcion = ''
        //Toastr.success('Pregunta creada EXITOSAMENTE')
        console.log("Guardado con exito")
      }
    }
    
  }
}
</script>

<style>
    .form {
    width: 530px;
    height: 400px;
    margin: auto;
    position: relative;
    }

    .clasificacion {
    width: 470;
    height: 25px;
    justify-content: center;
    }

    .textarea_descripcion{
    height: 165px;
    }

</style>





