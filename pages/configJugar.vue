   <template lang="html">
   <div class="contenedor">
      
      <div class="cabeceras">
         <v-btn class="btnDevolder animated bounceInDown delay-1s" fab small color="red"to="/">
              <v-icon>arrow_back</v-icon>
         </v-btn>
         <h1 class="animated bounceInDown">OCA GAME</h1> 
         <h2 class="animated bounceInDown delay-1s" style="color: greenyellow">¡Personaliza tu juego!</h2>
      </div>

      <div style="display: inline; width: 100%">
         <div class="animated bounceInLeft delay-1s" style="float: left; width: 68%">
            <div class="marginCard">
               <v-card color="cyan" height="6.5em">
                  <h2>Dimensiones del tablero</h2>
                  <div>
                     <label for="filas">Filas:</label>
                     <select class="spinner" id="filas" v-model.number="filas">
                        <option>4</option>
                        <option>5</option>
                        <option>6</option>
                        <option>7</option>
                        <option>8</option>
                     </select>
                  
                     <label for="columnas" style="">Columnas:</label>
                     <select class="spinner" id="columnas" v-model.number="columnas">
                        <option>4</option>
                        <option>5</option>
                        <option>6</option>
                        <option>7</option>
                        <option>8</option>
                     </select>
                  </div>
                  
               </v-card>
            </div>
            

            <div class="marginCard" style="">
               <v-card color="cyan" height="6.5em">
                  <h2>Número de jugadores</h2>

                  <label for="nroJugadores">Jugadores:</label>
                  <select class="spinner" id="nroJugadores" v-model.number="nroJugadores">
                     <option>2</option>
                     <option>3</option>
                     <option>4</option>
                  </select>
               </v-card>
            </div>
            
            <div class="marginCard">
               <v-card color="cyan" height="6.5em">
                  <h2>Color de jugadores</h2>
                  
                  <div class="colores">
                     <div style="margin-left: 1em" v-for="i in nroJugadores" :key="i">
                        <label for="colores">Jugador {{i}}:</label>
                        <select class="spinner" v-model="datos[i]" id="colores">
                           <option>Verde</option>
                           <option>Rojo</option>
                           <option>Azúl</option>
                           <option>Amarillo</option>
                        </select>
                     
                     </div>
                  </div>
               </v-card>
            </div>

            <div style="display: block">
               <v-btn round class="animated bounceInDown delay-1s" to="tablero" id="btnJugar">
                  <v-icon left>videogame_asset</v-icon>
                     Jugar
                  </v-btn>
            </div>
         
         </div>

         <div class="animated bounceInRight delay-1s" style="width: 30%; float: right; margin-right: 1em">
            <v-card class="form3 animated bounceInLeft" id="clas" color="cyan" style="overflow:scroll; overflow-x:hidden;">

               <h2>Clasificaciones</h2>

               <div v-if="vClasificaciones.length < 1">
                  <label>No hay clasificaciones creadas</label>
               </div>
               
               <div id="lista" v-for="clasi in vClasificaciones">
                  <v-checkbox v-model="selected" :label="`${clasi}`" :value="clasi"></v-checkbox>
               </div>
            
            </v-card>
            
         </div>
      </div>
      
       

      
      
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
let agregarPreguntas = db.ref('clasificaciones');


var bandera = 1;
let vClasificaciones = []; 


agregarPreguntas.orderByValue().on('value',function(snapshot){
  if(bandera == 1){
    bandera++;
  }else{
    vClasificaciones = [];
  }
  
  let jsonA = snapshot.val();
  for (let index in jsonA){
    vClasificaciones.push(index);
  }
    
})

export default {

  name: 'configJuego',
  firebase: {
    clasificaciones: agregarPreguntas
  },
  data() {
    return {
      filas: 4,
      columnas: 4,
      nroJugadores: 2,
      datos: ['jugador1', 'jugador2', 'jugador3', 'jugador4'],
      colores: ['Verde', 'Amarillo', 'Rojo', 'Azúl'],
      color: '',
      vClasificaciones,
      selected: []
    }
  },
  watch: {
    filas: function() {
      this.$store.commit('setNroFilas', this.filas)
    },
    columnas: function() {
      this.$store.commit('setNroColumnas', this.columnas)
    },
    nroJugadores: function() {
      this.$store.commit('setNroJugadores', this.nroJugadores)
    },
    datos: function() {
      for (let index = 1; index < this.datos.length; index++) {
        this.$store.commit('setColorJugador' + index, this.datos[index])
      }
    },
    clasificacion: function() {
       this.$store.commit('setClasificacion', this.selected[0])
    }
  },
  methods: {
    asignacionColor(color, numero) {
      this['jugador' + numero] = color
    },
    validar(){
      for (let i = 0; i < this.datos.length; i++) {
         for (let j = 0; j < this.datos.length; j++) {
            if(i != j){
               if(this.datos[i] == this.datos[j]){
                  Toastr.error('Se debe seleccionar un color distinto para cada jugador')
                  return;
               }else if(this.datos[i] === ""){
                  Toastr.error('Se debe seleccionar un color para cada jugador')
                  return;
               }
            }
         }
      }

      if(this.selected.length == 0){
         Toastr.error('Debe seleccionar una clasificación')
         return;
      }else if(this.selected.length > 1){
         Toastr.error('Solo se puede seleccionar una clasificación')
         return;
      }
      if(1==1){
         document.getElementById("btnJugar").disabled = true;
      }
      
   }
  }
}
</script>

<style>

.form3{
  
  height: 400px;
  border-radius: 5px; 
  padding: 1em;
  margin-left: 1em;
  vertical-align: middle;
}

.form3::-webkit-scrollbar {
	width: 11px;
}

.form3::-webkit-scrollbar-thumb {
	background: rgb(73, 73, 73);
	border-radius: 5px;
}

</style>
