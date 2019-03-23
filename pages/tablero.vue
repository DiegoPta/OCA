<template lang="en">
        <div class="contenedor">
            
                 <div>
                    <div v-for="f in filas" :key="f">
                        <div v-for="c in columnas" :key="c" class="celdas"></div>
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
        colorJugador1:"",
        colorJugador2:"",
        colorJugador3:"",
        colorJugador4:"" 
    }

  },methods:{
      cargar(){
          this.filas  =this.$store.getters.getNroFilas,
          this.columnas  =this.$store.getters.getNroColumnas,
          this.nroJugadores  =this.$store.getters.getNroJugadores,
          this.colorJugador1  =this.$store.getters.getColorJugador1,
          this.colorJugador2  =this.$store.getters.getColorJugador2,
          this.colorJugador3  =this.$store.getters.getColorJugador3,
          this.colorJugador4  =this.$store.getters.getColorJugador4


      }
  }
}
</script>

<style>
    

</style>
