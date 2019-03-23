<template lang="html">
   <div class="contenedor">
      
      <div class="cabeceras">
         <h1>¡Personaliza tu juego!</h1> 
      </div>

      <div>
         <div class="marginCard">
            <v-card color="cyan" height="8em">
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
               
                  <label for="columnas" style="margin-left: 10em">Columnas:</label>
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
         

         <div class="marginCard">
            <v-card color="cyan" height="8em">
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
            <v-card color="cyan" height="8em">
               <h2>Color de jugadores</h2>
               
               <div class="colores">
                  <div style="margin-left: 2em" v-for="i in nroJugadores" :key="i">
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
      
      </div>
      <div style="margin-top: 2em">
         <v-btn to="tablero" class="">Jugar</v-btn>
      </div>
      
   </div>
   
</template>

<script>
export default {
  name: 'configJuego',
  data() {
    return {
      filas: 4,
      columnas: 4,
      nroJugadores: 2,
      datos: ['jugador1', 'jugador2', 'jugador3', 'jugador4'],
      colores: ['Verde', 'Amarillo', 'Rojo', 'Azúl'],
      color: ''
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
    }
  },
  methods: {
    asignacionColor(color, numero) {
      this['jugador' + numero] = color
    }
  }
}
</script>

<style>

</style>
