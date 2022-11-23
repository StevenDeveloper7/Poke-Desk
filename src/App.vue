<template>
<div class="">
  <NavBar />
  <br><br>
  <div class="container-fluid">
    <div class="row mt-5">
      <div class="col-md-3 col-sm-12">
        <label class="label-text" for="">¿Cuantos pokemones deseas ver?</label>
        <div class="input-group mb-3">
          <input class="form-control" type="number" v-model="cant">
          <button @click="getPokemons()" class="input-group-text btn btn-outline-success" ><i class="bi bi-search"></i></button>
          <button @click="before()" class="btn btn-outline-primary" >Anterior</button>
          <button @click="next()" class="btn btn-outline-primary" >Siguiente</button>
        </div>
      </div>
    </div>
    <card :pokemons="pokemons" />
  </div>
  <footer></footer>
</div>

</template>


<script>
import Card from './components/Card.vue';
import NavBar from './components/NavBar.vue';
export default {
    components: { NavBar, Card },
    
    mounted(){
      this.getPokemons();
      // this.getPokemonDetails();
    },

    data: () => ({
      pokemons: {},
      show: "",
      cant: 15,
      ofs: 0
    }),

    methods: {
     async getPokemons(){
        const cant = this.cant;
        const ofs = this.ofs;
        const res = await fetch(`https://pokeapi.co/api/v2/pokemon?limit=${cant}&offset=${ofs}`);
        const data = await res.json();
        const pokemons = data.results;
        const poke = [];

        for (let i = 0; i < pokemons.length; i++) {
          const ab = []; 
          const mv = []; 

          const res2 = await fetch(pokemons[i].url)
          const details = await res2.json();
          const abilit = details.abilities;
          const moves = details.moves;
          const limit = 5;
          for (let s = 0; s < abilit.length; s++) {
            const dataAbilities = {
              id: s+1,
              name: abilit[s].ability.name
            } 
            ab.push(dataAbilities);         
          }

          for (let t = 0; t < moves.length; t++) {
            const dataMoves = {
              id: t+1,
              name: moves[t].move.name
            } 
            if (t < 5 ) {
             mv.push(dataMoves);         
            }
          }
          const data1 = {
            name:  pokemons[i].name.toUpperCase(),
            xp: details.base_experience,
            height: details.height,
            image: details.sprites.other.home.front_default,
            ability: details.abilities[0].ability.name,
            abilities: ab,
            moves: mv
          }
          poke.push(data1);
        }
        this.pokemons = poke;
      },
      async getPokemonDetails(){
        const res = await fetch("https://pokeapi.co/api/v2/pokemon/1");
        const data = await res.json();
      },

      next(){
        this.ofs+=this.cant;
        this.getPokemons()
      },
      before(){
        if (this.ofs > 0) {
          this.ofs-=this.cant;
          this.getPokemons()
        }
        
      }
    },
  };
</script>


