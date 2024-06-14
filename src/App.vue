<template>
  <div id="app">
    <Puntaje :score = "score"
      :intentos = "intentos"
      :message="message"
      :showReset="showReset"
      :isWinner="isWinner"
      @reiniciar_game="reiniciar"
    />
    <Dinamica v-if="!showReset" @actualizar_puntaje = "actualizar"/>
      
  </div>


</template>

<script>
import Dinamica from './components/Dinamica.vue';
import Puntaje from './components/Puntaje.vue';

export default{

        components:{
            Dinamica,
            Puntaje,
        },
        data(){
          return{
            score: 0,
            intentos: 5,
            message: '',
            showReset: false,
            isWinner: false,
          };
        },
        methods: {
    actualizar(points) {
      this.score += points;
      this.intentos -= 1;
      if (this.score >= 10) {
        this.message = `Puntaje: ${this.score}\nFelicitaciones has ganado un premio de $10.000,00`;
        this.isWinner = true;
        this.showReset = true;
        
      } else if (this.intentos === 0) {
        this.message = 'Haz utilizado tus 5 intentos\nEl juego ha terminado, inténtalo nuevamente';
        this.isWinner = false;
        this.showReset = true;
      }
    },
    reiniciar() {
      this.score = 0;
      this.intentos = 5;
      this.message = '';
      this.showReset = false;
      this.isWinner = false;
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>