<template>
  <div id="app">
    <!-- <img src="./assets/logo.png"> -->
    <Search
    @getList="getPlayList"
    />
    <Playlist
      v-for="comp in components"
      :songsPar="songsPar"
    />
  </div>
</template>

<script>

import Search from './components/Search'
import Playlist from './components/Playlist'
import axios from 'axios';

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
            pic: 'http://devtest.qiniudn.com/Preparation.jpg'
          };
          this.songsPar.push(song);
        }
        // console.log("sss");
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
