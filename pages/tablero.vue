<template lang="en">
        <div class="contenedor">

            <div class="cabeceras">
                <h1>OCA GAME</h1> 
            </div>
            
            <div style="display: flex">
                <div style="display: inline-block; width: 16em; margin: 1em">
                    <h2 style="display: inline">Info de partida</h2>
                    <div>
                        <div class="bloque">Jug.</div>
                        <div class="bloque">Color/Posición</div>
                    </div>
                    <div style="display: table-row" v-for="i in nroJugadores" :key="i">
                        <div class="bloque">Jugador {{i}}</div>

                        <div v-if="colores[i] == 'Verde'" style="background-color: green" class="bloque">1</div>
                        <div v-else-if="colores[i] == 'Rojo'" style="background-color: red" class="bloque">1</div>
                        <div v-else-if="colores[i] == 'Azúl'" style="background-color: blue" class="bloque">1</div>
                        <div v-else style="background-color: yellow" class="bloque">1</div>
                    </div>

                </div>

                <div style="display: inline-block; width: 40em">
                    <div v-for="f in filas" :key="f" class="tablero">
                        <div v-for="c in columnas" :key="c" class="celdas"></div>
                    </div>
                </div>

                <div style="display: inline-block; width: 16em; margin: 1em">
                    <img src="@/static/images/dado.png">
                </div>
            </div>
            
            
           
            
        </div>



</template>

<script>
export default {
    beforeMount(){
        this.cargar();
    }, 
  data(){
    return{
        filas:10,
        columnas:10,
        nroJugadores:2,
        colores: []
    }

  },methods:{
      cargar(){
          this.filas  =this.$store.getters.getNroFilas,
          this.columnas  =this.$store.getters.getNroColumnas,
          this.nroJugadores  =this.$store.getters.getNroJugadores,
          this.colores[1]  =this.$store.getters.getColorJugador1,
          this.colores[2]  =this.$store.getters.getColorJugador2,
          this.colores[3]  =this.$store.getters.getColorJugador3,
          this.colores[4]  =this.$store.getters.getColorJugador4


      }
  }
}
</script>

<style>
    

</style>
