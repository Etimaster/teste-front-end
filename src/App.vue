<template>
  <div>
    <div v-if="assitirVideo.data.items.length == 0">
      <busca v-on:reultadoBusca="getReultados" v-bind:indice="indice"/>
      <resultados v-on:carregarMais="infinitScroll" v-on:abrirVideo="mostrarVideo" v-bind:resultado="videosMostrados" v-bind:carregando="carregando"/>
      <falha v-if="mostrarFalha"/>
    </div>
    <videoPlayer v-else v-on:closeVideo="reset" v-bind:videoData="assitirVideo.data.items[0]"/>
  </div>
</template>

<script>
import axios from "axios";

import videoPlayer from './components/videoPlayer.vue'
import busca from './components/busca.vue'
import resultados from './components/resultados.vue'
import falha from './components/falha.vue'

const URL = 'https://www.googleapis.com/youtube/v3/';
const KEY = 'AIzaSyBQ7XFlMJvHNrYBBb2U4Kd5-a22LRVq2a4';

export default {
  name: 'iCasei',
  data(){
    return{
      resultadoBusca : {data:{items:[]}},
      videosMostrados : [],
      assitirVideo : {data:{items:[]}},
      indice: "",
      mostrarFalha: false,
      nextPageToken: "CAkQAA",
      carregando: false
    }
  },
  components: {
    videoPlayer,
    busca,
    resultados,
    falha
  },
  methods: {
    async getReultados(busca){
      this.indice = busca.indice
      let url_search = URL + 'search' ;

      let searchParams = {
        params: {
          part: 'id,snippet',
          q: busca.indice,
          key: KEY,
          type: "video",
          maxResults: 9,
        }
      };

      this.resultadoBusca = await axios.get(url_search, searchParams)
      this.nextPageToken = this.resultadoBusca.data.nextPageToken
      this.videosMostrados = this.resultadoBusca.data.items
    },
    async infinitScroll(){
      this.carregando = true;
      let url_search = URL + 'search' 
      let searchParams = {
        params: {
          part: 'id,snippet',
          q: busca.indice,
          key: KEY,
          maxResults: 9,
          type: "video",
          pageToken: this.nextPageToken
        }
      };

      let novaBusca = await axios.get(url_search, searchParams)
      let novosVideos = novaBusca.data.items
      this.videosMostrados = this.videosMostrados.concat(novosVideos);
      this.nextPageToken = novaBusca.data.nextPageToken

      this.carregando = false;
    },
    async mostrarVideo(video){
      let url_video = URL + 'videos';

      let videoParams = {
        params: {
          part: 'snippet,statistics',
          id: video.id,
          key: KEY
        }
      }
      
      this.assitirVideo = await axios.get(url_video, videoParams);
    },
    reset(){
      this.assitirVideo = {data:{items:[]}}
    },
  },
  watch:{
    videosMostrados(){
      this.mostrarFalha = this.indice !== "" && this.videosMostrados.length === 0
    }
  },
}
</script>

<style>
</style>
