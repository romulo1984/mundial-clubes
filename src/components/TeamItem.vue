<template>
  <div class="media">
    <img v-if="badgeSide === 'left'" :src="team.fields.badge.fields.file.url" class="mr-2 align-self-center" :alt="team.fields.name" width="40">
    <div class="media-body align-self-center">
      <h5 class="m-0" style="font-weight: 100">{{ team.fields.name }}</h5>
    </div>
    <img v-if="badgeSide === 'right'" :src="team.fields.badge.fields.file.url" class="ml-2 align-self-center" :alt="team.fields.name" width="40">
  </div>
</template>

<script>
export default {
  name: 'TeamItem',
  props: {
    team: Object,
    badgeSide: {
      type: String,
      default: 'left'
    }
  }
}
</script>

<style scoped>
  * {
    font-family: 'Roboto', sans-serif;
    font-weight: 100;
  }
  @media (max-width: 575px) {
    h5 {
      font-size: 16px;
    }
    img {
      width: 25px;
    }
  }
</style>
