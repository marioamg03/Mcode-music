<template  lang="pug">
  li.artist
    h2: a(:href="artist.url" target="_blank") {{ artist.name }}
    img(:src="artist.image[2]['#text']")
</template>

<script>
export default {
  name:'artist',
  props:['artist']
}
</script>

<style lang="stylus" scoped>
  @import url('https://fonts.googleapis.com/css?family=Permanent+Marker');
  li.artist
    font-family: 'Permanent Marker'
    cursive
    display inline-block
    margin 10px 100px 100px 10px
  li.artist img
    border-radius: 50%
  li.artist img:hover
      box-shadow: 0 0 4px 3px rgba(76,0,112, 0.5);
</style>
