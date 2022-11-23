<template>
    <Transition name="modal">
    <div v-if="show && modal" class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
          <div class="modal-header">
            <button class="modal-default-button" @click="close">OK</button>
            <img :src="pokemonDetails.image" height="360" alt="">
          </div>

          <div class="modal-body">
            <slot name="body">
                <h3 class="text-center">{{pokemonDetails.name}}</h3>
                <div class="row text-center">
                    <div class="col-md-4">
                        <h5>Ataque: {{pokemonDetails.ability}}  </h5>
                    </div>
                    <div class="col-md-4">
                        <h5>XP base:<br>  {{pokemonDetails.xp}}  </h5>
                    </div>
                    <div class="col-md-4">
                        <h5>Altura:<br>  {{pokemonDetails.height}}  </h5>
                    </div>
                </div><br>
                <div class="row ">
                    <div class="col-md-6">
                        <h5 text-center>Habilidades</h5>
                        <li v-for="ability in pokemonDetails.abilities" :key="ability.id">{{ability.name}}</li>
                    </div>
                    <div class="col-md-6">
                        <h5 text-center>Movimientos</h5>
                        <li v-for="moves in pokemonDetails.moves" :key="moves.id">{{moves.name}}</li>

                    </div>
                </div>
            </slot>
          </div>

          <div class="modal-footer">
            <slot name="footer">
              default footer
              
            </slot>
          </div>
        </div>
      </div>
    </div>
  </Transition>
</template>
<script>
export default{
    props:{
    show: Boolean,
    pokemonDetails: Object
    },
    
    data: () =>({
        modal: true
    }),
    methods: {
        close(){
        this.modal = false;
        },
    }
}    

    
</script>

<style>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 500px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  float: right;
}
.modal-enter-from {
  opacity: 0;
}

.modal-leave-to {
  opacity: 0;
}

.modal-enter-from .modal-container,
.modal-leave-to .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>