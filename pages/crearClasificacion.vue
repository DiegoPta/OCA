<template lang="html">
    
    <div class="contenedor">
      <v-layout  d-block >
        <div class="cabeceras">
            <v-btn class="btnDevolder animated bounceInLeft" fab small color="red"to="agregarContenido">
              <v-icon>arrow_back</v-icon>
          </v-btn>
            <h1 class="animated bounceInDown">Crear clasificacion</h1>
        </div>

        <v-flex xs12 sm8 md6>

            <v-card class="form animated bounceInDown" color="cyan" >
                <v-card-title class="headline"></v-card-title>

                  <v-text-field
                  class="clasificacion"
                  :counter="80"
                  maxlength="80"
                  v-model="clasificacion"
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
                  v-model="descripcion"
                  label="Descripcción"
                  required>
                  </v-textarea>

                  <v-btn round class="btns" @click="addClasificacion" v-bind:disabled="clasificacion === ''">
                    <v-icon left>save</v-icon>
                    Guardar
                    </v-btn>
                  <v-btn round class="btns" v-on:click="clear">
                    <v-icon left>clear</v-icon>
                    Limpiar
                    </v-btn>

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

  let vClas = []; 

  agregarClas.once('value').then( function(snapshot){
      let jsonA = snapshot.val();
      for (let index in jsonA){
        vClas.push(index)
      }
  })

  

export default {
  
  firebase: {
    clasificaciones: agregarClas
  },

  data() {
    return {
      descripcion: '',
      clasificacion : ''
    }
  },

  methods: {
    clear() {
      this.clasificacion = ''
      this.descripcion = ''
      Toastr.success('Limpiado')
    },
    addClasificacion() { 

      if(vClas.includes(this.clasificacion.toLowerCase())){
          Toastr.error('Ya existe una clasificación con el nombre ingresado');
      }else if ( this.descripcion == ''){
          Toastr.error('Hay algun campo vacio');
      } else{
        let agregarClas = db.ref('clasificaciones/'+this.clasificacion);
        agregarClas.set({
            descripcion: this.descripcion
          });
        this.clasificacion = ''
        this.descripcion = ''
        Toastr.success('Clasificación creada exitosamente');
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





