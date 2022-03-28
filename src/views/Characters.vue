<template>
  <h3> {{ character.name}} </h3>
  <img :src="character.image" alt="">
  <div class="character__info">
      <h4> {{ character.status}} </h4>
      <div class="status">
        <span
          :class="
            character.status == 'Alive' ? 'alive' :
            character.status == 'Dead' ? 'dead' :
            'default'"
        ></span>
        <span>{{ character.status }} - {{ character.species }}</span>
      </div>
      <div class="origen">
        <span>
          Origin: 
          {{ character.origin.name }}
        </span>
      </div>
      <div class="location">
        <span>
          Location: 
          {{ character.location.name }}
        </span>
      </div>
    </div>
</template>

<script>
 export default {
   data() {
     return {
       character: {}
     }
   },
   methods: {
     async mostrarCharacterPorId() {
      try {
        const data = await fetch(`https://rickandmortyapi.com/api/character/${this.$route.params.id}`);
        const getCharacterid = await data.json();
        this.character = getCharacterid;
        console.log(this.character);
      
      } catch (error) {
        console.log(error);
        throw error;
      }
     }
   },
   created() {
     this.consumirCharacterPorId();
   }
 }
</script>

<style scoped>

.character {
  background-color: var(--background-card);
  border-radius: 20px;
  box-shadow: 0 0 10px 1px var(--background-body);
  overflow: hidden;
  cursor: pointer;
  transition: transform 200ms ease-in-out;
  height: 100%;
}
h3 {
      color: var(--text-orange);
}
span {
    color: var(--text-gray);
}
h3 {
    margin-bottom: 0.5rem;
}
.status{
   display: flex;
   align-items: center;
   margin-bottom: 0.5rem;
 } 
.alive {
    background-color: green;
}
.dead {
    background-color: red;
}
.default {
    background-color: white;
}
    
.origen {
      margin-bottom: 0.5rem;
}


</style>