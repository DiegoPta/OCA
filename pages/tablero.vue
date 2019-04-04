<template lang="en">
        <div class="contenedor">

            <div class="cabeceras">
                <h1>OCA GAME</h1> 
            </div>
            
            <div>
                <div style="float: left; vertical-align: middle; display: inline-block; width: 16em; margin: 1em">
                    <div style="display: table-cell">
                        <h2 style="display: table-row">Información</h2>
                        

                        <div style="display: table-row">
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
                    

                </div>

                <div style="vertical-align: middle; display: inline-block">
                    <div v-for="f in filas" :key="f">
                        <div v-for="c in columnas" :key="getNumero(f,c)"  class="tablero">
                            <div>
                                <div v-if="getNumero(f,c) == (filas * columnas)" class="llegada">{{getNumero(f,c)}}<br>Meta</div>
                                <div v-else-if="getNumero(f,c) == 1" class="salida">{{getNumero(f,c)}}<br>Inicio</div>
                                <div v-else class="celdas">{{getNumero(f,c)}}</div>
                            </div>
                        </div>
                    </div>
                </div>

                <div style="margin: 1em; float: right; display: inline-block; vertical-align: middle">
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
            filas:4,
            columnas:4,
            nroJugadores:2,
            colores: []
        }

    },
    methods:{
        cargar(){
            this.filas  =this.$store.getters.getNroFilas,
            this.columnas  =this.$store.getters.getNroColumnas,
            this.nroJugadores  =this.$store.getters.getNroJugadores,
            this.colores[1]  =this.$store.getters.getColorJugador1,
            this.colores[2]  =this.$store.getters.getColorJugador2,
            this.colores[3]  =this.$store.getters.getColorJugador3,
            this.colores[4]  =this.$store.getters.getColorJugador4
        },
        getNumero(f, c){
            if(f%2 == 0){
                return (this.filas * this.columnas + 1) - ((this.columnas * (f-1)) + (this.columnas - c +1)) ;
            }else {
                if(f > 1){
                    return (this.filas * this.columnas + 1) - ((this.columnas * (f-1)) + c);
                }else{
                    return (this.filas * this.columnas + 1) - c;
                }
            }
        }
    }
}
</script>

<style>
    

</style>
