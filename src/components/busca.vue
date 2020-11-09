<template>
  <div class="container">
    <div class="row justify-content-sm-center">
      <div class="col col-sm-8">
        <form :class="resultado" id="busca-video">
          <div class="form-group">
            <input v-model="novoIndice" type="text" id="busca-video-input" class="form-control align-middle" placeholder="Pesquisar">
            <button v-on:click.prevent="buscar" type="submit" id="busca-video-submit" class="align-middle">
              <svg width="1em" height="1em" viewBox="0 0 16 16" class="bi bi-search" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" d="M10.442 10.442a1 1 0 0 1 1.415 0l3.85 3.85a1 1 0 0 1-1.414 1.415l-3.85-3.85a1 1 0 0 1 0-1.415z"/>
                <path fill-rule="evenodd" d="M6.5 12a5.5 5.5 0 1 0 0-11 5.5 5.5 0 0 0 0 11zM13 6.5a6.5 6.5 0 1 1-13 0 6.5 6.5 0 0 1 13 0z"/>
              </svg>
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default{
  props: ["indice"],
  data(){
    return {
      resultado: "busca",
      novoIndice: this.indice
    }
  },
  methods: {
    buscar() {
      if(this.novoIndice.trim() !== ""){
        this.$emit('reultadoBusca', {
          indice: this.novoIndice
        });

        this.resultado = "resultados"
      }
    }
  },
  created() {
    console.log(this.indice);
    if(this.indice !== ""){
      this.resultado = "resultados"
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  @keyframes formAnim {
    0% {margin-top: calc(50vh - 22px);}
    100% {margin-top: 5vh;}
  }

  #busca-video{
    height: 44px;
    margin-top: 5vh;
  }

  #busca-video.busca{
    margin-top: calc(50vh - 22px);
  }

  #busca-video.resultados{
    animation-name: formAnim;
    animation-duration: 0.5s;
  }

  input{
    display: inline-block;
    width: 90%;
    border: 2px solid #000;
    border-right: 0;
    border-radius: 0;
    padding: 20px 0px 20px 20px;
  }

  input:focus{
    border-color: #000;
    box-shadow: 0 0 0 0;
  }

  button{
    display: inline-block;
    width: 10%;
    height: 44px;
    border: 2px solid #000;
    border-left: 0;
    background-color: white;
  }

  button:focus{
    border-left: 0;
    outline: 0;
  }

  @media only screen and (min-width: 720px) {
    input{
      width: 95%;
    }

    button{
      width: 5%;
    }
  }
</style>
