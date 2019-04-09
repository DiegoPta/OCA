<template lang="html">
    
    <div class="contenedor">
        <v-layout  d-block>
            <div class="cabeceras">
                <h1 class="animated bounceInDown delay-1s">OCA GAME</h1>
            </div>
            <div>
                <img class="animated bounceInDown" src="@/static/images/oca.png">
            </div>

            <div style="">
                <v-btn class="animated bounceInDown delay-1s" to="configJugar">Jugar</v-btn>
            </div>
                
            <div>
                <v-btn class="animated bounceInDown delay-1s" to="agregarContenido">Agregar contenido</v-btn>
            </div>

        </v-layout>
    </div>
    
</template>

<script>
export default {}
</script>

<style lang="css">
</style>
