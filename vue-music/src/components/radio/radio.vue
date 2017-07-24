<template>
  <transition name="slide">
    <music-list :songs="songs" :title="title" :bg-image="bgImage"></music-list>
  </transition>
</template>

<script>
  import {mapGetters} from 'vuex'
  import {getRadioDetail} from 'api/recommend'
  import {ERR_OK} from 'api/config'
  import {createSong} from 'common/js/song'
  import MusicList from 'components/music-list/music-list'

  export default {
    data () {
      return {
        songs: []
      }
    },
    created () {
      this._getRadioDetail()
      console.log(this.radio)
    },
    methods: {
      _getRadioDetail () {
        if (!this.radio.dissid) {
          this.$router.push('/recommend')
          return
        }
        getRadioDetail(this.radio.dissid).then((res) => {
          if (res.code === ERR_OK) {
            this.songs = this._normallizeSongs(res.cdlist[0].songlist)
          }
        })
      },
      _normallizeSongs (list) {
        let ret = []
        list.forEach((item) => {
          if (item.songid && item.albummid) {
            ret.push(createSong(item))
          }
        })

        return ret
      }
    },
    computed: {
      title () {
        return this.radio.dissname
      },
      bgImage () {
        return this.radio.imgurl
      },
      ...mapGetters([
        'radio'
      ])
    },
    components: {
      MusicList
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "~common/stylus/variable"

  .slide-enter-active, .slide-leave-active
    transition: all 0.3s
  .slide-enter, .slide-leave-to
    transform: translate3d(100%, 0, 0)
</style>
