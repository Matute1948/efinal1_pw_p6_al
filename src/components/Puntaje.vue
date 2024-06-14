<template>
    <div class="puntaje">
        <div class="info" v-if="!showReset">
            <p>Puntaje: {{ score}}</p>
            <p>Intentos: {{ intentos}}</p>
            
        </div>
        <div v-else class="message-final" :class="{'win': isWinner, 'lose': !isWinner}">
            <p>{{ message }}</p>
            <button @click="resetGame" v-if="showReset">Nuevo Juego</button>
        </div>
        
    </div>
  </template>
  
  <script>
  export default {
    props: ['score', 'intentos', 'message', 'showReset', 'isWinner'],
    methods: {
      resetGame() {
        this.$emit('reiniciar_game');
      }
    }
  };
  </script>
  
  <style>
  .puntaje {

    text-align: center;
  }
  .win {
    color: blue;
    font-size: 3em;
    margin-top: 20%;
  }
  .lose {
    color: red;
    font-size: 3em;
    margin-top: 20%;
  }
  .info{
    display: grid;
    grid-template-columns: 1fr 1fr;
    
  }
  .mensaje-final {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: rgba(255, 255, 255, 0.9);
  text-align: center;

}
.mensaje-final p {

  font-size: 2em;
  margin-bottom: 20px;
}

  </style>