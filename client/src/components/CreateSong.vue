<template>
  <v-layout>
    <v-flex xs4>
      <panel title="Song Metadata">
        <v-text-field
        v-model="title"
        label="Title"
        ></v-text-field>

        <v-text-field
        v-model="song.artist"
        label="Artist"
        ></v-text-field>

        <v-text-field
        v-model="song.genre"
        label="Genre"
        ></v-text-field>

        <v-text-field
        v-model="song.album"
        label="Album"
        ></v-text-field>

        <v-text-field
        v-model="song.albumImageUrl"
        label="Album Image URL"
        ></v-text-field>

        <v-text-field
        v-model="song.youtubeId"
        label="Youtube ID"
        ></v-text-field>
      </panel>
    </v-flex>

    <v-flex xs8>
      <panel title="Song Structure" class="ml-2">
        <v-text-field
        v-model="song.tab"
        label="Tab"
        multi-line
        ></v-text-field>

        <v-text-field
        v-model="song.lyrics"
        label="Lyrics"
        multi-line
        ></v-text-field>
      </panel>
        <v-btn
          dark
          class="blue"
          @click="create">
          Create Song
        </v-btn>
    </v-flex>
  </v-layout>
</template>

<script>
import Panel from '@/components/Panel'
import SongsService from '@/services/SongsService'
export default {
  data () {
    return {
      song: {
        title: null,
        artist: null,
        genre: null,
        album: null,
        albumImageUrl: null,
        youtubeId: null,
        lyrics: null,
        tab: null
      }
    }
  },
  methods: {
    async create () {
      try {
        await SongsService.post(this.song)
        this.$router.push({
          name: 'songs'
        })
      } catch (err) {
        console.log(err)
      }
    }
  },
  components: {
    Panel
  }
}

</script>
<style scoped>

</style>
