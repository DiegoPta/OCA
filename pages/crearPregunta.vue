
<template lang="html">
    
    <div class="contenedor">
        <v-layout  d-block>
            <div class="cabeceras">
                <h1>Crear Pregunta</h1>
            </div>


      <v-flex xs12 sm8 md6>
      <div class="text-xs-center"></div>
      <v-card class="form">
        <v-card-title class="headline">Crear pregunta</v-card-title>

        <v-textarea
          class="textarea_pregunta"
          outline
          maxlength="200"
          :counter="200"
          :rules="preguntaRules"
          v-model="agregarPregunta.pregunta"
          label="Formula tu pregunta"
          required
        ></v-textarea>
        <br>
        <br>
        <br>
        <br>

        <v-text-field
          class="opciones"
          :counter="80"
          maxlength="80"
          :rules="opcionesRules"
          v-model="agregarPregunta.opcionRespuesta"
          label="Respuesta"
          outline
          required
        ></v-text-field>

        <v-text-field
          class="opciones"
          :counter="80"
          maxlength="80"
          :rules="opcionesRules"
          v-model="agregarPregunta.opcionA"
          label="Opcion A"
          outline
          required
        ></v-text-field>

        <v-text-field
          class="opciones"
          :counter="80"
          maxlength="80"
          :rules="opcionesRules"
          v-model="agregarPregunta.opcionB"
          label="Opcion B"
          outline
          required
        ></v-text-field>

        <v-text-field
          class="opciones"
          :counter="80"
          maxlength="80"
          :rules="opcionesRules"
          v-model="agregarPregunta.opcionC"
          label="Opcion C"
          outline
          required
        ></v-text-field>

        <v-text-field
          class="opciones"
          :counter="80"
          maxlength="80"
          :rules="opcionesRules"
          v-model="agregarPregunta.opcionD"
          label="Opcion D"
          outline
          required
        ></v-text-field>

        <v-btn  @click="addPreguntas">Guardar</v-btn>
        <v-btn  v-on:click="clear">Limpiar</v-btn>
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
let agregarPreguntas = db.ref('preguntas');

export default {
  
  firebase: {
    preguntas: agregarPreguntas
  },

  data() {
    return {
      agregarPregunta: {
        pregunta: '',
        opcionRespuesta: '',
        opcionA: '',
        opcionB: '',
        opcionC: '',
        opcionD: ''
      },
      preguntaRules: [v => !!v || 'Este campo es requerido'],
      opcionesRules: [v => !!v || 'Este campo es requerido']
    }
  },

  methods: {
    clear() {
      pregunta: this.agregarPregunta.pregunta = ''
      opcionRespuesta: this.agregarPregunta.opcionRespuesta = ''
      opcionA: this.agregarPregunta.opcionA = ''
      opcionB: this.agregarPregunta.opcionB = ''
      opcionC: this.agregarPregunta.opcionC = ''
      opcionD: this.agregarPregunta.opcionD = ''
    },
    addPreguntas() { 
      agregarPreguntas.push(this.agregarPregunta); 
      pregunta: this.agregarPregunta.pregunta = ''
      opcionRespuesta: this.agregarPregunta.opcionRespuesta = ''
      opcionA: this.agregarPregunta.opcionA = ''
      opcionB: this.agregarPregunta.opcionB = ''
      opcionC: this.agregarPregunta.opcionC = ''
      opcionD: this.agregarPregunta.opcionD = '' 
    }
  }
}
</script>

<style >

.form {
  width: 530px;
  height: 750px;
  margin: auto;
  position: relative;
}

.textarea_pregunta {
   width: 470px;
   height: 90px;
}

.opciones {
  width: 470px;
  height: 90px;
}

</style>