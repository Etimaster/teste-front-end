<template>
  <div class="container" id="results">
    <div class="row" id="results">
      <div class="col col-md-4" v-for="(video, index) in resultado" v-bind:key="index">
        <div :id="video.id.videoId" class="video" v-on:click="abrirVideo">
          <img class="img-fluid" :src="video.snippet.thumbnails.high.url"/>
          <h5 class="title">{{ video.snippet.title }}</h5>
          <h6>{{ video.snippet.channelTitle }}</h6>
          <p>{{ video.snippet.description }}</p>
          <button>Detalhes do video</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default{
  props: ["resultado", "carregando"],
  created () {
    window.addEventListener('scroll', this.handleScroll);
  },
  destroyed () {
    window.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    abrirVideo(event) {
      this.$emit('abrirVideo', {
        id: event.currentTarget.id
      });
    },
    handleScroll () {
      if(!this.carregando){
        let fimDaPagina = document.documentElement.scrollTop + window.innerHeight === document.documentElement.offsetHeight;

        if(fimDaPagina){
          this.$emit('carregarMais');
        } 
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .container{
    margin-top: 40px;
  }

  .col{
    margin-bottom: 40px;
  }

  .video{
    cursor: pointer;
  }

  img{
    margin-bottom: 10px;
  }

  .title{
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
  }

  button{
    text-transform: uppercase;
    border: 0;
    padding: 10px 20px;
    border-radius: 0;
    background-color: #ddd;
  }
  button:focus{
    border: 0;
    outline: 0;
  }
</style>