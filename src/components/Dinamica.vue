<template>
    <div class="container-juego">
        <div class="cuadros">
            <div v-for="(cuadro, index) in cuadros" :key="index" class="cuadro">
                <img :src="cuadro.img" alt="Error al cargar la imagen">
                <p>{{cuadro.nom}}</p>
            </div>
            
        </div>
        <button v-on:click="obtenerPokemones"> Jugar </button>
    </div>
</template>

<script>
export default{
    data() {
        return {
            cuadros: [
                {img:'https://via.placeholder.com/250 ',nom:'XXXXXXXXXXXXXXXXXXXXXXXX'},
                {img:'https://via.placeholder.com/250 ',nom:'XXXXXXXXXXXXXXXXXXXXXXXX'},
                {img:'https://via.placeholder.com/250 ',nom:'XXXXXXXXXXXXXXXXXXXXXXXX'}
            ],
            pokemones: [1,4,7,10,13],
        }
    },
    methods: {
        async obtenerPokemones(){
            
            const obtenerPokemones = [];
            for (let i = 0; i < 3; i++) {
                const idRan = this.pokemones[Math.floor(Math.random()*this.pokemones.length)];
                const data = await fetch(`https://pokeapi.co/api/v2/pokemon/${idRan}`).then(resp => resp.json());
                const {name} = data;
                obtenerPokemones[i] = {
                    img : `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${idRan}.svg`,
                    nom : name 
                }
                console.log(obtenerPokemones)   
            }
            this.cuadros = obtenerPokemones;
            this.$emit('actualizar_puntaje',this.calcularPuntaje(obtenerPokemones))
            
        },
        calcularPuntaje(cuadros){
            for(let i = 0; i<3 ; i++){
                let con = 0;
                for(let j=0; j<3; j++){
                    if (cuadros[i].nom===cuadros[j].nom) {
                        con++;
                    }
                }
                if (con === 2 ) {
                    return 2;
                }
                if (con === 3) {
                    return 5;
                }
            }
            return 0;
        },
    },
}
</script>

<style>

.container-juego {
  text-align: center;
}
.cuadros {
  display: flex;
  justify-content: center;
}
.cuadro {
  margin: 10px;
  text-align: center;
}
img{
    width: 250px;
    height: 250px;
}
</style>

