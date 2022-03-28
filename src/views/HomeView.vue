<template>
  <div class="container  mt-5">
    <h2 class="fst-italic text-center mb-5">Rick and Morty</h2>
    <div class="row" >
      <div v-for="character of characters" :key="character.id" class="col-sm-12 col-md-4">
        <h3>{{character.name}}</h3> 
        <!--personaje-->
        <img :src="character.image" alt="">
        <router-link :to="`/characters/${character.id}`">Personaje</router-link>
        <p>{{ character.body }}</p>
        <button  @click= personaje(character.id)></button>
        <hr/>
      </div>
    </div>

  </div>
</template>

<script>
// @ is an alias to /src  

export default {
  name: 'HomeView',
  components: {
  },
  data() {
    return {
      characters: [],
      charactersid: [],
    }
  },
  methods: {
    async consumirCharacter() {
      try {
        const data = await fetch('https://rickandmortyapi.com/api/character');
        const getcharacter = await data.json();
        this.characters = getcharacter.results;
        console.log(this.characters)
      } catch (error) {
        console.log(error);
        throw error;
      }
    },
    
  },
  created() {
    this.consumirCharacter();
  }
}
</script>

<style scope>

@import url('https://fonts.googleapis.com/css2?family=Amiri:ital,wght@1,700&display=swap" rel="stylesheet');

.container {
  height: 100vh;
  display: flex;
  justify-content: center;
 
}
h1 {
  font-family: 'Syne Mono', monospace;
  background-color: white;
  width: 900px;
  border-radius: 5px;
  border: 1px solid #000;
}
.cards {
  background: #fff;
  margin-top: 20px;
  margin-bottom: 0;
  margin-right: 20px;
  border-radius: 7px;
  border: 1px solid #000;
  box-shadow: 0 0px 10px 0 rgba(0,0,0,0.4);
  
  
}
.card-body {
  font-size: 14px;
  color: darkgray; 
  font-family: 'Hubballi', cursive;
}
.card-img-top {
  margin-top: 8px;
}
.btn {
  font-size: 14px;
  margin-top: 8px;
  margin-bottom: 0px;
  font-family: 'Syne Mono', monospace;
}
</style>
