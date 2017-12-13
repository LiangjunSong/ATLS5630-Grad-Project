<style src="../node_modules/vuetify/dist/vuetify.min.css">

</style> --> <style scoped> #inspire {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    /*margin-top: 60px;*/
}

#search-btn {
    margin-top: 10px;
}

</style>

<template>
  <div id="app">
    <!-- <img src="./assets/logo.png"> -->
    <v-app id="inspire">
        <v-container fluid="fluid" class="text-xs-center">
            <v-layout row wrap>
              <Search
              @getList="getPlayList"
              />
              <v-flex xs12 sm8 offset-sm2>
                <div class="wrapper" width="640">
                  <canvas class="visualizer" width="640" height="100"></canvas>
                </div>
              <Playlist
                v-for="comp in components"
                v-if="comp === index"
                v-bind:key="comp"
                :songsPar="songsPar"
              />
              <!-- <a-player :music="songsPar" ref="player"></a-player> -->
              </v-flex>
              <!-- <Player>
              </Player> -->

          </v-layout>

      </v-container>
    </v-app>
  </div>

</template>

<script>

import Search from './components/Search';
import Playlist from './components/Playlist';
import VueAplayer from 'vue-aplayer';
// import Player from './components/Player';
import axios from 'axios';
import draw from './script/draw.js';
import image from "./assets/album.jpg"

export default {
  name: 'app',
  components: {
    Search,
    Playlist,
    'a-player': VueAplayer
    // Player
  },

  data() {
      return {
          songsPar:[{
            title: 'Preparation',
            author: 'Hans Zimmer/Richard Harvey',
            url: 'http://devtest.qiniudn.com/Preparation.mp3',
            pic: 'http://devtest.qiniudn.com/Preparation.jpg',
            lrc: '[00:00.00]lrc here\n[00:01.00]aplayer'
          }],
          components: 1,
          index: 1
      }
  },
  mounted() {
      console.log("mounted");
      draw();
      /*

      ThreeJs custom waves
      Original script by ThreeJS : https://threejs.org/examples/canvas_particles_waves.html
      Modified version for Cloudoru by Kevin Rajaram : http://kevinrajaram.com
      Date: 08/14/2014


      */

  },
  methods: {
    getPlayList(tags) {
      var url = "http://api.napster.com/v2.2/search/verbose?apikey=OWRkODNjNGYtNDAwMy00N2JiLWEwOWQtNzRhMzE3NjMyZmM5&query="
      for(var i = 0; i <tags.length; i++){
        if(i == 0 ){
          url = url + tags[i];
        }else{
          url = url + "+" + tags[i];
        }
      }
      console.log(url);
      axios.get(url)
      .then(response => {
        // JSON responses are automatically parsed.
        //console.log(response.data.search.data.tracks);
        console.log(response.data);
        //var tracks = response.data.search.data.tracks;
        var playlist = response.data.search.data.playlists[0];
        var playlistUrl = playlist.href + "/tracks?apikey=OWRkODNjNGYtNDAwMy00N2JiLWEwOWQtNzRhMzE3NjMyZmM5&limit=10";
        console.log(playlistUrl);
        console.log(playlist.images[0].url);
        axios.get(playlistUrl)
        .then(response => {
          var tracks = response.data.tracks;
          console.log(tracks);
          this.songsPar = [];
          for(var i = 0; i < tracks.length; i++){
            var song = {
              title: tracks[i].name,
              author: tracks[i].artistName,
              url: tracks[i].previewURL,
              pic: playlist.images[0].url
            };
            this.songsPar.push(song);
          }
          this.components ++;
          this.index ++;
        });
        // this.songsPar = [];
        // for(var i = 0; i < tracks.length; i++){
        //   var song = {
        //     title: tracks[i].name,
        //     author: tracks[i].artistName,
        //     url: tracks[i].previewURL,
        //     pic: playlist.images[0].url
        //   };
        //   this.songsPar.push(song);
        // }
        // this.components ++;
        // this.index ++;
        console.log(this.songsPar);
      })
    }
  }
}
</script>

<style>
/*#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}*/
</style>
