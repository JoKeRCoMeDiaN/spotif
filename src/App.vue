<template>
  <div id="app">
   <header>
        <h1>Great Music</h1>
   </header>
   <main>
      <section class="player">
        <h2 class="song-title">{{ current.title }} - <span>{{ current.artist }}</span></h2>
        <div class="control">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">pause</button>
          <button class="next" @click="next">Next</button>
        </div>
        </section>
        <section class="playlist">
          <h3>The Playlist</h3>
          <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'song playing' : 'song'">
            {{ song.title }} - {{song.artist}}
          </button>
          </section>   
    </main>  
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
      return {
        current: {},
        index: 0,
        isPlaying: false,
        songs: [
        {
          title: 'Eng',
          artist: 'Lijpe',
          src: require('./assets/Lijpe - Eng (prod. Djermo).mp3')
        },
        {
          title: 'Unforgettable',
          artist: 'French Montana',
          src: require('./assets/French Montana - Unforgettable ft. Swae Lee.mp3')
        },
        {
          title: 'Rockstar',
          artist: 'Post Malone',
          src: require('./assets/Post Malone - Rockstar feat. 21 Savage Official Audio.mp3')
        },
        {
          title: 'Dont Rush',
          artist: 'Young T & Bugsey',
          src: require('./assets/Young T & Bugsey - Dont Rush Lyrics ft Headie One.mp3')
        },
        {
          title: 'THE SCOTTS',
          artist: 'Travis Scott, Kid Cudi',
          src: require('./assets/THE SCOTTS, Travis Scott, Kid Cudi - THE SCOTTS (Audio).mp3')
        },
        {
          title: 'London',
          artist: 'Tion Wayne',
          src: require('./assets/London (feat. Tion Wayne).mp3')
        },
        {
          title: 'Haters',
          artist: 'Fredo ft. Not3s',
          src: require('./assets/Haters - Fredo ft. Not3s (Lyrics).mp3')
        },
        {
          title: 'Enge Loesoe',
          artist: 'JoeyAK ft. Drechter & 3robi',
          src: require('./assets/JoeyAKEnge Loesoe ft. Drechter &amp 3robi (prod. JasonXM).mp3')
        },
        {
          title:  'Kassa',
          artist: 'LA$$A. Ashafar',
          src: require('./assets/Kassa.mp3')
        },
        {
          title: 'Hood Rich',
          artist: 'Josylvio ft. Alrima (prod. Monsif)',
          src: require('./assets/Josylvio - Hood Rich ft. Alrima (prod. Monsif).mp3')
        },
        {
          title:  'PAPERCHASE',
          artist: 'BOEF (Prod. Southbeats)',
          src: require('./assets/BOEF - PAPERCHASE (Prod. Southbeats).mp3')
        },
        {
          title:  'OP DE WEG',
          artist: 'JACK (PROD. ASIAH)',
          src: require('./assets/JACK - OP DE WEG (PROD. ASIAH).mp3')
        },
        ],
        player: new Audio()
      }
  },
  methods: {
    play (song) {
      if (typeof song.src != "undefined") {
       this.current = song; 

       this.player.src =this.current.src;
      }

      this.player.play();
      this.player.addEventListener('ended', function () {
        this.index++;

        if (this.index > this.songs.length - 1) {
        this.index = 0;
      }

    this.current = this.songs[this.index];
    this.play(this.current);
      }.bind(this));
      this.isPlaying = true;
    },
    pause () {
      this.player.pause();
      this.isPlaying = false;
    },
   next () {
    this.index++;
    if (this.index > this.songs.length - 1) {
      this.index = 0;
    }

    this.current = this.songs[this.index];
    this.play(this.current);
   },
   prev () {
     this.index--;
    if (this.index < 0) {
      this.index = this.songs.length -1;
    }

    this.current = this.songs[this.index];
    this.play(this.current);
   },
  },
  created () {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: sans-serif;
}
header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #fff;
}
main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}

.song-title {
  color: #53565a;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}

.song-title span {
  font-weight: 400;
  font-style: italic;

}

.control {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}

button {
  appearance: none;
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
}

button:hover {
  opacity: 0.8;
}

.play, .pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #fff;
  background-color: deepskyblue;
}

.next, .prev {
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #fff;
  background-color: rgb(34, 156, 197);
}

.playlist {
  padding: 0px 30px;
}
.playlist h3 {
  color: #212121;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}
.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}

.playlist .song:hover {
  color: rgb(8, 85, 250);
}

.playlist .song.playing {
  color: #fff;
  background-image: linear-gradient(to right, rgb(179, 201, 247), rgb(8, 85, 250));
}
</style>
