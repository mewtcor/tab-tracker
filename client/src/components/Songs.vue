<template>
  <v-layout column>
    <v-layout wrap>
      <v-flex xs6 offset-xs3>
        <panel title="Songs">
          <v-btn
            slot="action"
            @click="navigateTo({name: 'songs-create'})"
            class="cyan accent-2"
            light
            medium
            absolute
            right
            middle
            fab>
            <v-icon>add</v-icon>
          </v-btn>
          <div
            v-for="song in songs"
            :key="song.id">
            {{song.title}} |
            {{song.artist}} |
            {{song.genre}} |
            {{song.album}} |
            {{song.albumImageUrl}} |
            {{song.youtubeId}}
            {{song.lyrics}}
            {{song.tab}}
          </div>
        </panel>
      </v-flex>
    </v-layout>
  </v-layout>
</template>

<script>
import SongsService from '@/services/SongsService'
import Panel from '@/components/Panel'
export default {
  components: {
    Panel
  },
  data () {
    return {
      songs: null
    }
  },
  methods: {
    navigateTo (route) {
      this.$router.push(route)
    }
  },
  async mounted () {
    this.songs = (await SongsService.index()).data
  }
}
</script>
<style scoped>

</style>
