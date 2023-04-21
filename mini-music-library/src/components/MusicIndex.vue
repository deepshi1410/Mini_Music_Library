<!-- This component is used to serve our music-->
<!-- pagination is used to show only a small piece of data so that problem of showing a large piece of data at once
and re-rendering it once data is changed is not at all good for website performance -->
<template>
  <table
    class="table is-bordered is-striped is-narrow is-hoverable is-fullwidth"
  >
  <sorted :songs="songs" @sortedSongs="sort_songs"></sorted>
  <paginated :records="sortedList" />
  </table>
</template>
<script>
import MusicData from '@/assets/list.json'
import PaginatedTableData from '@/components/PaginatedTableData.vue'
import SortMusic from '@/components/SortMusic.vue'
export default {
  components: {
    'paginated': PaginatedTableData,
    'sorted': SortMusic
  },
  data () {
    return {
      songs: MusicData,
      sortedList: MusicData
    }
  },
  methods: {
    sort_songs (data) {
      this.sortedList = data
    }
  }
}
</script>

<style lang="scss" scoped></style>
