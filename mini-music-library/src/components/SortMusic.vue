<template>
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
</template>

<script>
export default {
  props: {
    songs: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      sortBy: '',
      sortDirection: 'asc'
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
      // calling sorting the songss method
      this.sort_songs()
    },
    sort_songs () {
      if (this.sortBy === '') {
        this.$emit('sortedSongs', this.songs)
        return
      }
      let sortModifier = this.sortDirection === 'asc' ? 1 : -1
      let sortedList = this.songs.slice().sort((a, b) => {
        let columnA = a[this.sortBy].toUpperCase()
        let columnB = b[this.sortBy].toUpperCase()
        if (columnA > columnB) {
          return 1 * sortModifier
        } else if (columnA === columnB) {
          return 0
        } else {
          return -1 * sortModifier
        }
      })
      return sortedList
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
