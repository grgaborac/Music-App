<template>
  <div class="container">
    <div class="songName">
      <img v-bind:src="songs[pl_index].imgSrc" alt="Artist Picture" class="image" v-if="playing">
      <h3 v-if="!playing">Choose a song!</h3>
      <h3 v-else>{{ songPlaying }}</h3>
    </div>

    <div class="buttons">
      <button class="prev" @click="prevSong">Prev</button>
      <button class="state" v-if="!playing" @click="playSongButton">Play</button>
      <button class="state" v-else @click="pauseSong">Pause</button>
      <button class="next" @click="nextSong">Next</button>
    </div>

    <h1>The Playlist</h1>

    <ul>
      <li v-for="str in songs" :key="str" @click="playSong(str.name)" :class="{active: str.active}">
        <h3>{{ str.artist }} - {{ str.name }}</h3>
      </li>
    </ul>    

  </div>
</template>

<script>
export default {
  data: function() {
    return {
      playing: null,
      songPlaying: '',
      pl_index: 0,

      current: {},
      player: new Audio(),

      songs: [{artist: 'Alex Figueira', 
      name: 'Silky', 
      active: false, 
      src: require('../assets/silky.mp3'),
      imgSrc: require('../assets/f1.jpg')
      },
      {artist: 'Caslo', 
      name: 'Freedom', 
      active: false, 
      src: require('../assets/freedom.mp3'),
      imgSrc: require('../assets/casloimg.jpg')
      },
      {artist: 'Jules FK', 
      name: 'Hello Bob', 
      active: false, 
      src: require('../assets/helloBob.mp3'),
      imgSrc: require('../assets/julesfkimg.jpg')}
      ]
    }
  },
  methods: {
    playSong: function(name) {
      this.activeState()
      this.pl_index = this.songs.indexOf(this.songs.find(x => x.name === name))
      this.songPlaying = this.songs[this.pl_index].artist + ' - ' + this.songs[this.pl_index].name 
      this.playing = true
      this.songs[this.pl_index].active = true

      this.play()
      
    },
    play: function() {
      this.player.src = this.songs[this.pl_index].src
      this.player.play()
    },
    activeState: function() {
      this.songs[this.pl_index].active = false
    },
    playSongButton: function() {
      this.songPlaying = this.songs[this.pl_index].artist + ' - ' + this.songs[this.pl_index].name 
      this.songs[this.pl_index].active = true
      this.playing = true
      this.play()
    },
    pauseSong: function() {
      this.activeState()
      this.playing = false
      this.player.pause()
    },
    nextSong: function() {
      this.songs[this.pl_index].active = false
      this.pl_index++;

      if(this.pl_index > this.songs.length - 1){
        this.pl_index = 0;
      }
      this.songPlaying = this.songs[this.pl_index].artist + ' - ' + this.songs[this.pl_index].name 
      this.songs[this.pl_index].active = true
      this.playing = true
      this.play()
    },
    prevSong: function() {
      this.songs[this.pl_index].active = false
      this.pl_index--;

      if(this.pl_index < 0){
        this.pl_index = this.songs.length - 1;
      }
      this.songPlaying = this.songs[this.pl_index].artist + ' - ' + this.songs[this.pl_index].name 
      this.songs[this.pl_index].active = true

      this.playing = true

      this.play()
    }
    }
}
</script>

<style>
.songName{
  width: 100%;
  height: 15vh;
  margin: 0 0 30px 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #0f0f0f;
  color: #fff;
}
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.buttons{
  width: 40vw;
  height: 10vh;
  margin: 8vh auto 5vh auto;
  padding-bottom: 40px;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  border-bottom: 1px solid #000;
}

.active{
  color: red;
}

.buttons button{
  font-size: 18px;
  margin: 0 2vw 0 2vw;
}

.state{
  font-size: 32px !important;
  padding: 10px;
}

h1{
  margin: 0 0 3vh 0;
}

ul{
  width: 18vw;
  display: inline-block;
  padding: 0 auto 0 50px;
}

li{
  padding: 2vh 0 2vh 0;
  width: 100%;
  border-bottom: 1px solid gray;
  list-style-type: none;
}

li:last-child{
  border-bottom: none;
}

.prev, .next{
  width: 5rem;
  height: 2.5rem;
}

.state{
  width: 8rem;
}
.image{
  border-radius: 50%;
  width: 100px;
  filter: brightness(0.9);
  position: absolute;
  left: 35vw;

}
</style>