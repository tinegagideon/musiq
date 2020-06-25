<template>
  <div id="app">
    <header>
      <h1>musiQ</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">
          {{current.title}} -
          <span>{{current.artist}}</span>
        </h2>
        <div class="controls">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3>Playlist</h3>
        <button
          v-for="song in songs"
          :key="song.src"
          @click="play(song)"
          :class="(song.src==current.src)?'song playing':'song'"
        >{{song.title}}-{{song.artist}}</button>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: "nexus",
          artist: "tyrell",
          src: require("./assets/tyrell - nexus.mp3")
        },
        {
          title: "sax pleasure",
          artist: "maya olson",
          src: require("./assets/maya olson - sax pleasure.mp3")
        },

        {
          title: "come over",
          artist: "lucky x lukies band",
          src: require("./assets/lucky x lukies band - come over.mp3")
        }
      ],
      player: new Audio()
    };
  },
  methods: {
    play(song) {
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    next() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    }
  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  /* outline: 1px solid purple; */
}
body {
  font-family: sans-serif;
}
header {
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
  padding: 20px 40px;
  background-color: antiquewhite;
}
main {
  width: 100%;
  max-width: 700px;
  margin: 0 auto;
}
.player {
  margin-top: 10px;
}
.song-title {
  color: #333;
  font-size: 1.4rem;
  font-weight: 600;
  text-align: center;
}
.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}
button {
  appearance: none;
  border: none;
  outline: none;
  cursor: pointer;
}
button:hover {
  background-color: whitesmoke;
}
.play,
.pause {
  font-size: 1em;
  padding: 8px 15px;
  margin: 0 15px;
  border-radius: 10px;
  background: antiquewhite;
}
.next,
.prev {
  font-size: 0.5em;
  padding: 8px 15px;
  margin: 0 15px;
  border-radius: 10px;
  background: antiquewhite;
}
.playlist {
  padding: 0 30px;
}
.playlist h3 {
  color: #333;
  font-size: 1.2em;
  margin-bottom: 30px;
  text-align: center;
}
.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
}
.playlist .song.playing {
  color: black;
  background-color: blanchedalmond;
}
</style>
 