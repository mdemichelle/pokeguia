<template>
  <div class="principal">
    <h1 style="text-align:center; font-size: xxx-large">PokeGuía</h1>
    <form action="">
      <label for="">Nombre:</label>
      <input type="text" v-model="character.name" />
      <input type="submit" value="Buscar" @click.prevent="fetchCharacter" />
    </form>

      <img :src="image.front_default" alt="no hay imagen" />
    <section class="info">
    
      
      <div class="caracteristicas">
            <div class="moves">
        <h3>Movimientos</h3>
        <ul>
          <li v-for="(movimiento, index) in movimientos" :key="index">
            {{ movimiento.move.name }}
          </li>
        </ul>
      </div>
      <div class="moves">
        <h3>Habilidades</h3>
        <ul>
          <li v-for="(habilidad, index) in habilidades" :key="index">
            {{ habilidad.ability.name }}
          </li>
        </ul>
      </div>
      </div>
    
    </section>
  </div>
</template>

<script>
export default {
  name: "component-pokemon",
  // props: {},
  data: function () {
    return {
      character: {
        name: "pikachu",
        movimiento: "",
        movimientos: [],
        habilidades: [],
        habilidad: "",
        sprites: {
          front_default: "",
        },
      },
    };
  },
  computed: {
    image() {
      return this.character.sprites;
    },

    movimientos() {
      return this.character.moves;
    },
    habilidades() {
      return this.character.abilities;
    },
  },
  methods: {
    fetchCharacter() {
      //peticion a API
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.character.name}`)
        //transforma la data a un json, se puede hacer un return en el then
        .then((response) => response.json()) //esto es igual a un return
        .then((json) => {
          console.log(json);
          this.character = json;
        })
        .catch((error) => {
          alert("El Pokemon que buscas no existe, intenta de nuevo");
          console.log(error);
        });
    },
  },
  // components: {},
  created(){
      this.fetchCharacter();
  }
};
</script>

<style scoped>
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Courier New', Courier, monospace;
}
.principal{
    display: flex;
    flex-direction: column;
    
}
.info{
    display: flex;
    justify-content: center;
}
.caracteristicas {
    
  width: 80%;  
  display: flex;
  justify-content: space-around;
}

img{
    align-self: center;
}
form{
    margin: 25px 0 40px 0;
    align-self: center;
}

</style>