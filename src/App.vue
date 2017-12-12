<template>
  <div id="app">
    <!-- <img src="./assets/logo.png"> -->
    <Search
    @getList="getPlayList"
    />
    <Playlist />
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
          songs:[]
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
        for(var i = 0; i < tracks.length; i++){
          var song = {
            title: tracks[i].name,
            author: tracks[i].artistName,
            url: tracks[i].previewURL,
            pic: ''
          };
          this.songs.push(song);
        }
        console.log(this.songs);
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
