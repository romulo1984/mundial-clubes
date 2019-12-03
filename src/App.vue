<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-12">
        <MatchesList :matches="items" v-for="(items, index) in matches" :key="index"/>
      </div>
    </div>
  </div>
</template>

<script>
import client from './config/contentful'
import MatchesList from './components/MatchesList'
import orderBy from 'lodash/orderBy'
import groupBy from 'lodash/groupBy'
import find from 'lodash/filter'

export default {
  name: 'app',
  props: {
    match: Number
  },
  components: {
    MatchesList
  },
  data () {
    return {
      matches: [],
      matchesIds: {
        1: 'GstcKWWlkz73QFHAWDzvT',
        2: '7zD3Tp3ngufDEbJsVDlcOz',
        3: '3CQPFKIXRk5vHjQ0Oj0jlC',
        4: '6XqLfbsnzgd5ABhfiHtl7w',
        5: '3z0dXymkf6G7COmYAVYftw',
        6: '5kf21JdU3UF0YB2M68qXzZ',
        7: '1soP4cp3GqZhs2Ywhbjsyu'
      }
    }
  },
  async created () {
    const matches = await client.getEntries({
      content_type: 'matches'
    })

    const matchId = this.match || this.getParameterByName('match')

    if (matchId) {
      this.matches.push(find(matches.items, { sys: { id: this.matchesIds[matchId] } }))
    } else {
      this.matches = orderBy(
        groupBy(matches.items, 'fields.phase.fields.order'),
        'fields.phase.fields.order'
      )
    }
  },
  methods: {
    getParameterByName (name, url) {
      if (!url) url = window.location.href
      name = name.replace(/[[\]]/g, '\\$&')
      const regex = new RegExp('[?&]' + name + '(=([^&#]*)|&|#|$)')
      const results = regex.exec(url)
      if (!results) return null
      if (!results[2]) return ''
      return decodeURIComponent(results[2].replace(/\+/g, ' '))
    }
  }
}
</script>

<style>
  @import url("https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css");
</style>
