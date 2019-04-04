<template lang="html">
    
    <div class="contenedor">
      <v-layout  d-block >
        <div class="cabeceras">
            <h1>Crear clasificacion</h1>
        </div>

        <v-flex xs12 sm8 md6>

            <v-card class="form" color="cyan" >
                <v-card-title class="headline"></v-card-title>

                  <v-text-field
                  class="clasificacion"
                  :counter="80"
                  maxlength="80"
                  v-model="agregarClasificacion.clasificacion"
                  label="Nombre de la clasificación"
                  outline
                  required
                  ></v-text-field>
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

                  <v-btn class="i nput_button" @click="addClasificacion">Guardar</v-btn>
                  <v-btn class="input_button" v-on:click="clear">Limpiar</v-btn>

              </v-card>
              
            </v-flex>
      </v-layout>
    </div>
    
</template>

<script>

import Firebase from 'firebase';
import Toastr from 'toastr';

let config = {
   apiKey: "AIzaSyB8-Gut27wxsuGdg1e7DyavWFgF60gnm8A",
    authDomain: "ocagame-bd.firebaseapp.com",
    databaseURL: "https://ocagame-bd.firebaseio.com",
    projectId: "ocagame-bd",
    storageBucket: "ocagame-bd.appspot.com",
    messagingSenderId: "131259496872"
}


 if (!Firebase.apps.length) {
    Firebase.initializeApp(config);
  } 
  let db = Firebase.database();
  let agregarClas = db.ref('clasificaciones');

export default {
  
  firebase: {
    clasificaciones: agregarClas
  },

  data() {
    return {
      agregarClasificacion: {
        clasificacion: '',
        descripcion: ''
      }
    }
  },

  methods: {
    clear() {
      this.agregarClasificacion.clasificacion = ''
      this.agregarClasificacion.descripcion = ''
      Toastr.success('Limpiado')
    },
    addClasificacion() { 
      if (this.agregarClasificacion.clasificacion == '' ||  this.agregarClasificacion.descripcion == ''){
          Toastr.error('Hay algun campo vacio')
      } else{
        agregarClas.push(this.agregarClasificacion); 
        this.agregarClasificacion.clasificacion = ''
        this.agregarClasificacion.descripcion = ''
        Toastr.success('Pregunta creada exitosamente')
      }
    }
    
  }
}
</script>

<style>
    .form {
    width: 530px;
    height: 370px;
    border-radius: 5px; 
    margin-left: 20em;
    margin-top: 4em;
    }

    .clasificacion {
    width: 485px;
    display: inline-block;
    }

    .textarea_descripcion{
    width: 485px;
    height: 165px;
    display: inline-block;
    }

</style>





