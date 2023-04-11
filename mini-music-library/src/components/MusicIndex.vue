<!-- This component is used to serve our music-->
<template>
  <table
    class="table is-bordered is-striped is-narrow is-hoverable is-fullwidth"
  >
    <thead>
      <th style="30%">Title</th>
      <th style="30%">Artist</th>
      <th style="20%">Album Type</th>
      <th style="20%">Release Date</th>
    </thead>
    <tbody v-for="(song, index) in songs" :key="index">
      <tr>
        <td>{{ song.track.name }}</td>
        <td>{{ song.track.artists[0].name }}</td>
        <td>{{ song.track.album.album_type }}</td>
        <td>{{ song.track.album.release_date }}</td>
      </tr>
    </tbody>
  </table>
</template>
/* eslint-disable */
<script>
import MusicData from '@/assets/list.json'
export default {
  data () {
    return {
      songs: MusicData,
      sortBy: '',
      sortDirection: 'asc'
    }
  }
}
</script>

<style lang="scss" scoped></style>
