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
              <Playlist
                v-for="comp in components"
                :songsPar="songsPar"
              />
              </v-flex>

          </v-layout>

      </v-container>
    </v-app>
    <div id="cube" style="width:400px; height:400px;">THREE.JS should appear here</div>
      <div id="cubeapp">

      </div>
  </div>

</template>

<script>

import Search from './components/Search'
import Playlist from './components/Playlist'
import axios from 'axios';
import * as THREE from 'three';
import image from "./assets/album.jpg"

export default {
  name: 'app',
  components: {
    Search,
    Playlist
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
      var scene = new THREE.Scene();
      var camera = new THREE.PerspectiveCamera( 75, 400 / 400, 0.1, 1000 );

      var renderer = new THREE.WebGLRenderer();
      renderer.setSize( 400, 400 );
      var geometry = new THREE.BoxGeometry( 1, 1, 1 );
      var material = new THREE.MeshBasicMaterial( { color: 0x00ff00, wireframe:true } );
      var cube = new THREE.Mesh( geometry, material );
      scene.add( cube );

      camera.position.z = 5;

      document.getElementById("cube").appendChild( renderer.domElement );
      function render() {
        requestAnimationFrame( render );
        renderer.render( scene, camera );
        cube.rotation.x += 0.01;
          cube.rotation.y += 0.01;
      }
      render();
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
        console.log(response.data.search.data.tracks);
        var tracks = response.data.search.data.tracks;
        this.songsPar = [];
        for(var i = 0; i < tracks.length; i++){
          var song = {
            title: tracks[i].name,
            author: tracks[i].artistName,
            url: tracks[i].previewURL,
            pic: image
          };
          this.songsPar.push(song);
        }
        this.components ++;
        this.index ++;
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
