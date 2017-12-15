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
  <a-player :music="songsPar" ref="player"></a-player>
</div>

</template>

<script>

import VueAplayer from 'vue-aplayer';
export default {
    name: 'Playlist',
    components:{
      'a-player': VueAplayer
    },
    // render: function (createElement) {
    //   // <div><slot :text="msg"></slot></div>
    //   return createElement('div', [
    //       'a-player', {
    //         props: {
    //           music: songsPar
    //         }
    //       }
    //   ])
    // },
    props: {
     songsPar: {
       type: Array,
       default () {
         return [{
           title: 'Preparation',
           author: 'Hans Zimmer/Richard Harvey',
           url: 'http://devtest.qiniudn.com/Preparation.mp3',
           pic: 'http://devtest.qiniudn.com/Preparation.jpg',
           lrc: '[00:00.00]lrc here\n[00:01.00]aplayer'
         }]
       }
     }
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
    beforeMount () {
      // console.log("Beofre mount");
      // console.log(this.songsPar);
    },

    mounted() {
        console.log("mounted");
        let aplayer = this.$refs.player.control;
        if (aplayer === null) {
          return;
        }
        aplayer.play();
    },
    updated () {
      // this.songs = this.songsPar; // save props data to itself's data and deal with it
      console.log("Update");
      // console.log(this.songsPar);
      let aplayer = this.$refs.player.control;
      console.log(aplayer);

      if (aplayer === null) {
        return;
      }
      aplayer.pause();
      aplayer.destroy();
    },
    beforeDestroy(){
      let aplayer = this.$refs.player.control;
      console.log(aplayer);

      if (aplayer === null) {
        return;
      }
      aplayer.pause();
      aplayer.destroy();
    }
}

</script>
