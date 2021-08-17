<template>
  <div>
    <div ref="ytplayer"></div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component
export default class extends Vue {
  vidId = 'M7lc1UVf-VE'

  mounted(): void {
    window.onYouTubeIframeAPIReady = () => {
      new YT.Player(this.$refs.ytplayer as HTMLElement, {
        videoId: this.vidId,
        playerVars: {
          playsinline: 1
        },
        events: {
          onReady(event: YT.PlayerEvent) {
            event.target?.playVideo()
          },
          onStateChange() {
            console.log('do something')
          }
        }
      })

      delete window.onYouTubeIframeAPIReady
    }

    const script = document.createElement('script')
    script.src = 'https://www.youtube.com/iframe_api'
    const firstScriptTag = document.getElementsByTagName('script')[0]
    firstScriptTag.parentNode?.insertBefore(script, firstScriptTag)
  }
}
</script>