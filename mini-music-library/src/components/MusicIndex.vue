<!-- This component is used to serve our music-->
<template>
  <table
    class="table is-bordered is-striped is-narrow is-hoverable is-fullwidth"
  >
    <thead>
      <th style="30%"><a @click="change_sort('name')">Name
        <fa-icon icon="chevron-up" v-if="sortBy == 'name' && sortDirection == 'asc'" />
        <fa-icon icon="chevron-down" v-if="sortBy == 'name' && sortDirection == 'desc'" /></a></th>
      <th style="30%"><a @click="change_sort('artist')">Artist
        <fa-icon icon="chevron-up" v-if="sortBy == 'artist' && sortDirection == 'asc'" />
        <fa-icon icon="chevron-down" v-if="sortBy == 'artist' && sortDirection == 'desc'" /></a></th>
      <th style="20%"><a @click="change_sort('album_type')">Album Type
        <fa-icon icon="chevron-up" v-if="sortBy == 'album_type' && sortDirection == 'asc'" />
        <fa-icon icon="chevron-down" v-if="sortBy == 'album_type' && sortDirection == 'desc'" /></a></th>
      <th style="20%"><a @click="change_sort('release_date')">Release Date
        <fa-icon icon="chevron-up" v-if="sortBy == 'release_date' && sortDirection == 'asc'" />
        <fa-icon icon="chevron-down" v-if="sortBy == 'release_date' && sortDirection == 'desc'" /></a></th>
    </thead>
    <tbody v-for="(song, index) in sortedList" :key="index">
      <tr>
        <td>{{ song.name }}</td>
        <td>{{ song.artist }}</td>
        <td>{{ song.album_type }}</td>
        <td>{{ song.release_date }}</td>
      </tr>
    </tbody>
  </table>
</template>
<script>
import MusicData from '@/assets/list.json'
export default {
  data () {
    return {
      songs: MusicData,
      sortBy: '',
      sortDirection: 'asc'
    }
  },
  computed: {
    sortedList () {
      if (this.sortBy === '') {
        return this.songs
      }
      let sortModifier = this.sortDirection === 'asc' ? 1 : -1
      return this.songs.slice().sort((a, b) => {
        console.log('a is' + a)
        let columnA = a[this.sortBy].toUpperCase()
        let columnB = b[this.sortBy].toUpperCase()
        console.log(columnA + ' ' + columnB)
        if (columnA > columnB) {
          return 1 * sortModifier
        } else if (columnA === columnB) {
          return 0
        } else {
          return -1 * sortModifier
        }
      })
    }
  },
  methods: {
    change_sort (column) {
      if (this.sortBy === column && this.sortDirection === 'asc') {
        this.sortDirection = 'desc'
      } else {
        this.sortDirection = 'asc'
      }
      this.sortBy = column
    }
  }
}
</script>

<style lang="scss" scoped></style>
