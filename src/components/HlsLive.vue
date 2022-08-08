<template>
  <video-player class="vjs-custom-skin"
    ref="videoPlayer"
    :options="playerOptions"
    @ready="playerReadied">
  </video-player>
</template>

<script>
import 'videojs-contrib-hls'

export default {
  name: 'hls-live',
  props: {
    src: {
      type: String,
      default: 'https://download.cloud.189.cn/file/downloadFile.action?dt=52&expired=1661272654316&sk=F5F475B8ED84DB5CAA0E8BCBF3542F53&ufi=31335116692257720&zyc=5&token=cloud16&sig=Zq5WHSuRXl8K94tZRXpekd8s0kk%3D'
    }
  },
  data () {
    return {
      playerOptions: {
        // height: '320',
        // width: '100%',
        sources: [{
          withCredentials: false,
          type: "application/x-mpegURL",
          src: this.src
        }],
        controlBar: {
          timeDivider: false,
          durationDisplay: false
        },
        flash: { hls: { withCredentials: false }},
        html5: { hls: { withCredentials: false }},
        autoplay: true, // 自动播放
        // controls: true, // 控制条
        fluid: true, // 按比例缩放适应容器
        // preload: 'auto', // 预加载
        // muted: true, // 消除所有音频
        // loop: false, // 循环播放
        aspectRatio: "16:9",
        // poster: 'https://surmon-china.github.io/vue-quill-editor/static/images/surmon-9.jpg' //首屏图片
      }
    }
  },
  methods: {
    playerReadied(player) {
      var hls = player.tech({ IWillNotUseThisInPlugins: true }).hls
      player.tech_.hls.xhr.beforeRequest = function(options) {
        // console.log(options)
        return options
      }
    }
  }
}
</script>
