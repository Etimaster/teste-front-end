<template>
  <div class="player">
    <div class="container">
      <div class="row">
        <div class="col">
          <h2>{{ videoData.snippet.title }}</h2>
          <iframe :src="'https://www.youtube.com/embed/' + videoData.id" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen/>
          <div class="details">
            <span class="canal">{{ videoData.snippet.channelTitle }}</span>
            <span class="deslike">
            <svg><path d="M15 3H6c-.83 0-1.54.5-1.84 1.22l-3.02 7.05c-.09.23-.14.47-.14.73v1.91l.01.01L1 14c0 1.1.9 2 2 2h6.31l-.95 4.57-.03.32c0 .41.17.79.44 1.06L9.83 23l6.59-6.59c.36-.36.58-.86.58-1.41V5c0-1.1-.9-2-2-2zm4 0v12h4V3h-4z" class="style-scope yt-icon" /></svg>
            {{ videoData.statistics.dislikeCount }}
            </span>
            <span class="like">
              <svg><path d="M1 21h4V9H1v12zm22-11c0-1.1-.9-2-2-2h-6.31l.95-4.57.03-.32c0-.41-.17-.79-.44-1.06L14.17 1 7.59 7.59C7.22 7.95 7 8.45 7 9v10c0 1.1.9 2 2 2h9c.83 0 1.54-.5 1.84-1.22l3.02-7.05c.09-.23.14-.47.14-.73v-1.91l-.01-.01L23 10z"/></svg>
              {{ videoData.statistics.likeCount }}
            </span>
          </div>
          <p class="descricao">{{ videoData.snippet.description }}</p>
          <span class="views">
            <svg width="1em" height="1em" viewBox="0 0 16 16" class="bi bi-eye-fill" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
              <path d="M10.5 8a2.5 2.5 0 1 1-5 0 2.5 2.5 0 0 1 5 0z"/>
              <path fill-rule="evenodd" d="M0 8s3-5.5 8-5.5S16 8 16 8s-3 5.5-8 5.5S0 8 0 8zm8 3.5a3.5 3.5 0 1 0 0-7 3.5 3.5 0 0 0 0 7z"/>
            </svg>
            {{ videoData.statistics.viewCount }}
          </span>
        </div>
      </div>
    </div>
    <button v-on:click.prevent="voltar" class="voltar">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="black" width="18px" height="18px"><path d="M0 0h24v24H0V0z" fill="none"/><path d="M15.41 16.59L10.83 12l4.58-4.59L14 6l-6 6 6 6 1.41-1.41z"/></svg>
    </button>
  </div>
</template>

<script>
export default{
  props: ["videoData"],
  methods: {
    voltar(){
      this.$emit('closeVideo');
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .player{
    position: relative;
  }

  .voltar{
    position: absolute;
    background-color: white;
    border: 2px solid black;
    border-radius: 0;
    top: 30px;
    left: 30px;
    font-weight: 900;
    padding-bottom: 4px;
    padding: 0 4px 4px;
  }

  span svg{
    height: 25px;
    width: 30px;
  }

  h2{
    margin: 30px 0;
    font-size: 22px;
  }

  iframe{
    width: 100%;
    height: 100%;
    margin-bottom: 20px;
  }

  .details{
    font-weight: 500;
  }

  span.canal{
    float: left;
  }

  span.like, span.deslike{
    float: right;
  }

  span.like{
    margin-right: 20px;
  }

  .descricao{
    display: inline-block;
    margin: 20px 0;
  }

  .views{
    font-weight: 500;
  }

</style>
