<template>
  <div id="app" class="everything">
    <header>
      Study and Chill
    </header>
      <main>
        <section class="player">
          <h2 class="current_song_title"> 
            {{ current.title }} - <span> {{ current.artist }} </span>
          </h2>
          <div class="buttons">
            <button class="previous" @click="previous">
              <img src="./assets/previous.png" style="heigth:25px;width:25px">
            </button>
            <button class="play" v-if="!isPlaying" @click="play">
              <img src="./assets/play.png" style="heigth:25px;width:25px">
            </button>
            <button class="pause" v-else @click="pause">
              <img src="./assets/pause.png" style="heigth:25px;width:25px">
            </button>
            <button class="next" @click="next">
              <img src="./assets/next.png" style="heigth:25px;width:25px">
            </button>
          </div>
        </section>
      </main>
  </div>
</template>
<script>
export default {
  name: 'app',
  data () {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songList: [
        {
          title: 'A Travelers Tale',
          artist: 'Tenno',
          src: require('./assets/ATravelersTale.mp3')
        },
        {
          title: 'Between Worlds',
          artist: 'Tenno',
          src: require('./assets/BetweenWorlds.mp3')
        },
        {
          title: 'Bushido',
          artist: 'Tenno',
          src: require('./assets/Bushido.mp3')
        },
        {
          title: 'Butterfly Lullaby',
          artist: 'Tenno',
          src: require('./assets/ButterflyLullaby.mp3')
        },
        {
          title: 'By Your Side',
          artist: 'Tenno',
          src: require('./assets/ByYourSide.mp3')
        },
        {
          title: 'Distant',
          artist: 'Shinobi Lite',
          src: require('./assets/Distant.mp3')
        },
        {
          title: 'Earth',
          artist: 'Michael Skaide',
          src: require('./assets/Earth.mp3')
        },
        {
          title: 'Kaya Village',
          artist: 'Tenno',
          src: require('./assets/KayaVillage.mp3')
        },
        {
          title: 'Kuro',
          artist: 'Nogymx & Tenno',
          src: require('./assets/Kuro.mp3')
        },
        {
          title: 'Lion Dance',
          artist: 'Aphrow',
          src: require('./assets/LionDance.mp3')
        },
        {
          title: 'Lost Grove',
          artist: 'Nogymx',
          src: require('./assets/LostGrove.mp3')
        },
        {
          title: 'Memories',
          artist: 'Shinobi Lite',
          src: require('./assets/Memories.mp3')
        },
        {
          title: 'Muramasa',
          artist: 'Tenno',
          src: require('./assets/Muramasa.mp3')
        },
        {
          title: 'The Seeker',
          artist: 'Tenno',
          src: require('./assets/TheSeeker.mp3')
        },
        {
          title: 'Yamabiko',
          artist: 'Tenno',
          src: require('./assets/Yamabiko.mp3')
        }
        
      ],
      player: new Audio()
    }
  },
  methods: {
    play (song) {
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.player.addEventListener('ended', function () {
        this.index++;
        if (this.index > this.songList.length - 1) {
          this.index = 0;
        }
        this.current = this.songList[this.index];
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
      if (this.index > this.songList.length - 1) {
        this.index = 0;
      }
      this.current = this.songList[this.index];
      this.play(this.current);
    },
    previous () {
      this.index--;
      if (this.index < 0) {
        this.index = this.songList.length - 1;
      }
      this.current = this.songList[this.index];
      this.play(this.current);
    }
  },
  created () {
    this.current = this.songList[this.index];
    this.player.src = this.current.src;
  }
}
</script>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}
body {
	font-family:"Arial";
  background: url(./assets/rsz_2background.jpg);
}
header {
	display: flex;
	justify-content: center;
	align-items: center;
	padding: 25px;
	color: pink;
  font-size: 48px;
  font-weight: bold;
  text-transform: uppercase;
}
main {
  width: 100%;
  max-width: 720px;
  margin: 0 auto;
  padding: 30px;
}
.current_song_title {
  font-size: 30px;
  font-weight: 650;
  color: pink;
  text-transform: uppercase;
  text-align: center;
  padding: auto;
  margin-top: 5%;
}
.buttons {
  display: flex;
  justify-content: center;
  margin-top: 7%;
}
.play, .pause {
  padding: 12px 24px;
  margin: 0px 12px;
  border-radius: 10px;
  background-color: #91009e;
}
.next, .previous {
  padding: 8px 16px;
  margin: 0px 8px;
  border-radius: 7px;
  background-color: #91009e;
}
button {
  border: none;
  outline: none;
  cursor: pointer;
}
button:hover {
  opacity: 0.9;
}

</style>
