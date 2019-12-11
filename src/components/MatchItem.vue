<template>
  <div class="match-item shadow">
    <div class="row">
      <div class="col-12 text-center small">
        <div class="match-item-datetime">
          {{ match.fields.arena }} |
          <span style="font-weight: 100">{{ moment(match.fields.datetime).format('dddd[,] DD/MM/YYYY [às] HH:mm') }}</span>
        </div>
      </div>
    </div>

    <div class="row d-flex justify-content-center pb-3 mt-3">
      <div class="col-sm-4 text-right mx-3 mx-sm-0">
        <TeamItem :team="match.fields.host" badge-side="right"/>
      </div>
      <div class="col-sm-1 col-4 align-self-center text-right py-2">
        <strong>{{ hostScore }}</strong>
      </div>
      <div class="col-sm-1 col-4 text-center align-self-center">x</div>
      <div class="col-sm-1 col-4 align-self-center py-2">
        <strong>{{ guestScore }}</strong>
      </div>
      <div class="col-sm-4 mx-3 mx-sm-0">
        <TeamItem :team="match.fields.guest"/>
      </div>
    </div>
  </div>
</template>

<script>
import TeamItem from './TeamItem'
import moment from 'moment'
moment.locale('pt-BR')

export default {
  name: 'MatchItem',
  props: {
    match: Object
  },
  components: {
    TeamItem
  },
  methods: {
    moment
  },
  computed: {
    guestScore () {
      return this.match.fields.guestScore === undefined ? '-' : this.match.fields.guestScore
    },
    hostScore () {
      return this.match.fields.hostScore === undefined ? '-' : this.match.fields.hostScore
    }
  }
}
</script>

<style lang="scss" scoped>
  * {
    font-family: 'Roboto', sans-serif;
  }
  .match-item {
    border: 1px solid rgba(0, 0, 0, .12);
    border-radius: 10px;
    margin-bottom: 15px;
    padding-top: 10px;
  }
  .match-item-datetime {
    font-size: 12px;
    @media (max-width: 575px) {
      position: relative;
      border: none;
      padding: 0 15px;
      font-size: 10px;
    }
  }
</style>
