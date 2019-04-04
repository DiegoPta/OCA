
<template lang="html">
    
  <div class="contenedor">
    <v-layout  d-block>
        <div class="cabeceras">
            <h1>Crear Pregunta</h1>
        </div>

  
      <v-card class="form2" color="cyan">

        <h2>Dilegenciar campos</h2>

        <v-textarea
          class="textarea_pregunta"
          outline
          maxlength="200"
          :counter="200"
          v-model="agregarPregunta.pregunta"
          label="Formula tu pregunta"
          required
        ></v-textarea>
            

        <v-text-field
          class="opciones"
          :counter="80"
          maxlength="80"
          v-model="agregarPregunta.opcionRespuesta"
          label="Respuesta (Debe ser igual a una opciones)"
          outline
          required
        ></v-text-field>

        <v-text-field
          class="opciones"
          :counter="80"
          maxlength="80"
          v-model="agregarPregunta.opcionA"
          label="Opcion A"
          outline
          required
        ></v-text-field>

        <v-text-field
          class="opciones"
          :counter="80"
          maxlength="80"
          v-model="agregarPregunta.opcionB"
          label="Opcion B"
          outline
          required
        ></v-text-field>

        <v-text-field
          class="opciones"
          :counter="80"
          maxlength="80"
          v-model="agregarPregunta.opcionC"
          label="Opcion C"
          outline
          required
        ></v-text-field>

        <v-btn  @click="addPreguntas">Guardar</v-btn>
        <v-btn  v-on:click="clear">Limpiar</v-btn>
      </v-card>

      <v-card class="form3" color="cyan">

        <h2>Clasicicaciones</h2>
          
        <div v-for="clasi in sel">
            <v-checkbox v-model="selected" :label="`${clasi}`" :value="clasi"></v-checkbox>
        </div>  
      </v-card>

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
let agregarPreguntas = db.ref('preguntas');
let buscarClasificaciones = db.ref('clasificaciones');

let vClasificaciones = []; 
let keyClas = [];


buscarClasificaciones.on('value', function(snapshot){
    let jsonA = snapshot.val();
    for (let index in jsonA){
      vClasificaciones.push(jsonA[index].clasificacion)
      keyClas.push(index)
    }

})




export default {
  
  firebase: {
    preguntas: agregarPreguntas,
    clasificaciones: buscarClasificaciones
  },

  data() {
    return {
      agregarPregunta: {
        pregunta: '',
        opcionRespuesta: '',
        opcionA: '',
        opcionB: '',
        opcionC: ''
      },
      sel : vClasificaciones,
      selected: []
    }
    
  },

  methods: {
    clear() {
      this.agregarPregunta.pregunta = ''
      this.agregarPregunta.opcionRespuesta = ''
      this.agregarPregunta.opcionA = ''
      this.agregarPregunta.opcionB = ''
      this.agregarPregunta.opcionC = ''
      Toastr.success('Limpiado')
    },
    addPreguntas() { 
       if (this.agregarPregunta.pregunta == '' || this.agregarPregunta.opcionRespuesta == '' || this.agregarPregunta.opcionA == '' || 
       this.agregarPregunta.opcionB == '' || this.agregarPregunta.opcionC == '' ){
          Toastr.error('Hay algun campo vacio')
        } else if (this.agregarPregunta.opcionRespuesta == this.agregarPregunta.opcionA || this.agregarPregunta.opcionRespuesta == this.agregarPregunta.opcionB || this.agregarPregunta.opcionRespuesta == this.agregarPregunta.opcionC ||
        this.agregarPregunta.opcionA == this.agregarPregunta.opcionB ||  this.agregarPregunta.opcionA == this.agregarPregunta.opcionC || 
        this.agregarPregunta.opcionB == this.agregarPregunta.opcionC ) {
          Toastr.error('Tiene opciones de respuestas repetidas')
        } else if(this.selected.length == 0){
          Toastr.error('No ha seleccionado ninguna clasificación')
        }else if(this.selected.length > 1){
          Toastr.error('Solo se puede seleccionar una clasificación')
        }else {
        agregarPreguntas.push(this.agregarPregunta); 
        pregunta: this.agregarPregunta.pregunta = ''
        opcionRespuesta: this.agregarPregunta.opcionRespuesta = ''
        this.agregarPregunta.opcionA = ''
        this.agregarPregunta.opcionB = ''
        this.agregarPregunta.opcionC = ''
        Toastr.success('Pregunta creada exitosamente')
        }
    }
  }
}
</script>

<style>

.form2 {
  width: 40%;
  border-radius: 5px; 
  /* margin-left: 20em;
  margin-top: -1em; */
  display: inline-block;
  padding: 2em;
  vertical-align: middle;
  margin: auto;
}

.form3{
  width: 30%;
  border-radius: 5px; 
  padding: 1em;
  margin-left: 10em;
  display: inline-block;
  vertical-align: middle;
}

.textarea_pregunta {
   width: 100%;
   display: inline-block;
}

.opciones {
  height: 90px;
  width: 100%;
  display: inline-block;
}

</style>