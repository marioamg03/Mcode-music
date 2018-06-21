<template  lang="pug">
  #app
    img(src='http://www.mariomendoza.com.ve/img/logo.png')
    h1 {{title}}
    select(v-model="selectedCountry")
     option(v-for="country in countries" v-bind:value="country.value") {{country.name}}
    spinner(v-show="loading")

    ul
      artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="artists.mbid")
</template>

<script>
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      artists:[],
      countries:[
        { name:'Argentina', value:'argentina' },
        { name:'Venezuela', value:'venezuela' },
        { name:'Canada', value:'canada' },
        { name:'Chile', value:'chile' }
      ],
      selectedCountry: 'spain',
      loading: true,
      title: 'MCode Music'
    }
  },
  components: {
    Artist,
    Spinner
  },
  methods:{
    refreshArtist(){
      const self = this
      this.loading = true
      this.artists = []
      getArtists(this.selectedCountry)
      .then(function (artists){
        self.loading = false
        self.artists = artists
      })
    }
  },
  mounted() {
    this.refreshArtist()
  },
  watch: {
    selectedCountry() {
      this.refreshArtist()
    }
  }
}
</script>

<style lang="stylus">
#app
	font-family 'Avenir', Helvetica, Arial, sans-serif
	-webkit-font-smoothing antialiased
	-moz-osx-font-smoothing grayscale
	text-align center
	color #2c3e50
	margin-top 60px
h1, h2
	font-weight normal
ul
	list-style-type none
	padding 0
li
	display inline-block
	margin 0 10px
a
	color #4C0070 !important

</style>
