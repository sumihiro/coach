<template lang="pug">
v-layout(column justify-center align-center)
  v-flex(xs12 sm8 md6)
    .text-center
      p.display-4.font-weight-black {{ current }}
    v-card
      v-card-text
        v-container(justify="center" py-0)
          v-layout(row wrap)
            v-flex(xs3)
              v-text-field(v-model="min" label="最小" type="number")
            v-flex(xs1)
            v-flex(xs3)
              v-text-field(v-model="max" label="最大" type="number")
            v-flex(xs1)
            v-flex(xs3)
              v-text-field(v-model="interval" label="間隔(ms)" type="number")
      v-card-actions
        v-spacer
          v-btn(color="primary" block @click="toggle")
            span(v-if="running") STOP
            span(v-if="!running") START
</template>

<script>
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'

export default {
  components: {
    Logo,
    VuetifyLogo
  },
  data () {
    return {
      running: false,
      min: 1,
      max: 10,
      interval: 1000,
      current: 0
    }
  },
  methods: {
    toggle () {
      this.running = !this.running
      if (this.running) {
        this.timer()
      }
    },
    timer () {
      if (this.running) {
        this.current = Math.floor(Math.random() * (this.max * 1 + 1 - this.min * 1)) + this.min * 1
        speechSynthesis.speak(new SpeechSynthesisUtterance(this.current))
        setTimeout(() => {
          this.timer()
        }, this.interval * 1)
      }
    }
  }
}
</script>
