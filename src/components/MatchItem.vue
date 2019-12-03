<template>
  <div class="match-item">
    <div class="row">
      <div class="col-12 text-center small">
        <div class="match-item-datetime">
          <strong>{{ match.fields.arena }}</strong> |
          {{ moment(match.fields.datetime).format('dddd[,] DD/MM/YYYY [às] HH:mm') }}
        </div>
      </div>
    </div>

    <div class="row d-flex justify-content-center pb-3 pt-4 mt-sm-4">
      <div class="col-sm-4 text-right mx-3 mx-sm-0">
        <TeamItem :team="match.fields.host" badge-side="right"/>
      </div>
      <div class="col-sm-1 col-4 align-self-center text-right py-2">
        <strong>{{ match.fields.hostScore || '-' }}</strong>
      </div>
      <div class="col-sm-1 col-4 text-center align-self-center">x</div>
      <div class="col-sm-1 col-4 align-self-center py-2">
        <strong>{{ match.fields.guestScore || '-' }}</strong>
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
  }
}
</script>

<style lang="scss" scoped>
  * {
    font-family: 'Roboto', sans-serif;
  }
  .match-item {
    border: 1px solid #ccc;
    border-radius: 10px;
    margin-bottom: 15px;
    padding-top: 10px;
  }
  .match-item-datetime {
    position: absolute;
    margin: 0 auto;
    top: -5;
    left: 0;
    right: 0;
    padding: 6px;
    border: 1px solid #ccc;
    border-radius: 6px;
    background-color: #fff;
    @media (max-width: 575px) {
      position: relative;
      border: none;
      padding: 0 15px;
      font-size: 10px;
    }
  }
</style>
