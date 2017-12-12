<style src="../../node_modules/vuetify/dist/vuetify.min.css">

</style> --> <style scoped> #inspire {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

#search-btn {
    margin-top: 10px;
}

</style>

<template>

<div>

  <a-player :music="songs" ref="player"></a-player>
</div>

</template>

<script>

import VueAplayer from 'vue-aplayer';
export default {
    name: 'Playlist',
    components:{
      'a-player': VueAplayer
    },
    data() {
        return {
          songs: [
              {
                title: 'Preparation',
                author: 'Hans Zimmer/Richard Harvey',
                url: 'http://devtest.qiniudn.com/Preparation.mp3',
                pic: 'http://devtest.qiniudn.com/Preparation.jpg',
                lrc: '[00:00.00]lrc here\n[00:01.00]aplayer'
              },
              {
                title: 'Preparation',
                author: 'Hans Zimmer/Richard Harvey',
                url: 'http://devtest.qiniudn.com/Preparation.mp3',
                pic: 'http://devtest.qiniudn.com/Preparation.jpg',
                lrc: '[00:00.00]lrc here\n[00:01.00]aplayer'
              },
              {
                title: 'Preparation',
                author: 'Hans Zimmer/Richard Harvey',
                url: 'http://devtest.qiniudn.com/Preparation.mp3',
                pic: 'http://devtest.qiniudn.com/Preparation.jpg',
                lrc: '[00:00.00]lrc here\n[00:01.00]aplayer'
              }
          ]
        }
    },
    mounted() {
        let aplayer = this.$refs.player.control;
        aplayer.play()
    }

}

</script>
