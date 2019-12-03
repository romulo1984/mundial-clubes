<template>
  <div class="mb-5">
    <h5 class="text-center text-uppercase">{{ matches[0].fields.phase.fields.name }}</h5>
    <MatchItem v-for="(match, index) in matches" :match="match" :key="index"/>
  </div>
</template>

<script>
import MatchItem from './MatchItem'

export default {
  name: 'MatchesList',
  props: {
    matches: Array
  },
  components: {
    MatchItem
  }
}
</script>

<style scoped>
  * {
    font-family: 'Roboto', sans-serif;
  }
</style>
