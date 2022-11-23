<template>
    <div class="row text-center">
        <div  v-for="pokemon in pokemons" :key="pokemon.name" class="card col-md-4 mt-3 mx-1 div-card" style="width: 18rem;">
        <img :src="pokemon.image" class="card-img-top  div-show" alt="">
            <div class="card-body">
              <h5 class="card-title">{{pokemon.name}}</h5>
              <div class="description">
                <p class="card-text">
                    <i class="bi bi-bag-heart-fill"></i>
                    XP: {{pokemon.xp}} <br> 
                    <i class="bi bi-arrow-up-right-circle-fill"></i>
                    Altura: {{pokemon.height}} <br> 
                    <i class="bi bi-cursor-fill"></i>
                    Ataque: {{pokemon.ability}}
                 </p>
              </div>
                <a href="#" @click="details(pokemon)" class="btn btn-outline-info  form-control"><i class="bi bi-search"></i></a>
            </div>
        </div>
    </div>
    <Transition name="modal">
    <div v-if="show" class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
            <div class="row">
            <button class="btn btn-outline-danger" @click="close"><i class="bi bi-backspace-reverse-fill"></i></button>
            </div>
          <div class="modal-header">
            
            <img :src="pokemonDetails.image" height="320" :alt="pokemonDetails.name">
          </div>

          <div class="modal-body">
            <slot name="body">
                <h3 class="text-center">{{pokemonDetails.name}}</h3>
                <div class="row text-center">
                    <div class="col-4">
                        <i class="bi bi-cursor-fill"></i>
                        <h5>Ataque: {{pokemonDetails.ability}}  </h5>
                    </div>
                    <div class="col-4">
                        <i class="bi bi-bag-heart-fill"></i>
                        <h5>XP base:<br>  {{pokemonDetails.xp}}  </h5>
                    </div>
                    <div class="col-4">
                        <i class="bi bi-arrow-up-right-circle-fill"></i>
                        <h5>Altura:<br>  {{pokemonDetails.height}}  </h5>
                    </div>
                </div><br>
                <div class="row ">
                    <div class="col-6">
                        <h5 text-center>Habilidades</h5>
                        <tr v-for="ability in pokemonDetails.abilities" :key="ability.id"><i class="bi bi-award"></i> {{ability.name}}</tr>
                    </div>
                    <div class="col-6">
                        <h5 text-center>Movimientos</h5>
                        <tr v-for="moves in pokemonDetails.moves" :key="moves.id"><i class="bi bi-arrows-fullscreen"></i> {{moves.name}}</tr>
                    </div>
                </div>
            </slot>
          </div>
        </div>
      </div>
    </div>
  </Transition>
</template>
 
<script>
export default {
    props:{
        pokemons: Object,
    },

    data: () => ({
        show: false,
        pokemonDetails: []
    }),
    methods:{
        details(pokemon){
            this.pokemonDetails = pokemon;
            this.show = true;
        },
        close(){
        this.show = false;
        },
        open(){
        this.show = true;
        },
    }
};
</script>

