<script>
import PlaylistService from './services/playlistService.js'
import SpotifyService from './services/spotifyService.js'

export default {

  data() 
  {
    return {
      playlistName : '',
      tracks: []
    }
  },

  methods : 
  {
    async showPlaylistName()
    {
      let spotifyService = new SpotifyService
      (
        'https://api.spotify.com/v1',
        'b39edce3f8614ddda8ab16b512f4d721',
        '4a496f2f89aa44c98e94fd62a424223f'
      )

      await spotifyService.loadToken()

      let playlistService = new PlaylistService(spotifyService)
      
      await playlistService.loadPlaylistData('2ZPCh3PYNhoar2UXf7nMov')

      this.playlistName = playlistService.playListName
      this.tracks = playlistService.tracks
    }
  }
}
</script>

<template>
  <body>
    <div class="wrapper">
      <button @click="showPlaylistName"> GET </button>
      <figure>
        <figcaption>{{ playlistName }} </figcaption>
        <ul>
          <li v-for="track in tracks">
          {{ track['track']['name'] }} : {{ track['track']['id'] }} 
          </li>
        </ul>
        </figure>
    </div>
  </body>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

span 
{
  color : 'white'
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
