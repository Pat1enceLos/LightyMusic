<template>
  <div class="audioControl no-drag">
    <div class="playbutton">
      <Icon type="pre" class="pre" @mouseup.native="handlePreAudio"></Icon>
      <Icon type="play" class="play" @mouseup.native="handleMouseup" v-show="paused"></Icon>
      <Icon type="pause" class="pause" @mouseup.native="handleMouseup" v-show="!paused"></Icon>
      <Icon type="next" class="next" @mouseup.native="handleNextAudio"></Icon>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';
import Icon from '../BaseIconContainer';

export default {
  name: 'AudioControl',
  data() {
    return {
    };
  },
  computed: {
    ...mapGetters(['paused', 'src', 'nextAudio']),
  },
  components: {
    Icon,
  },
  methods: {
    handleMouseup() {
      if (this.src) {
        this.$store.dispatch('updatePaused', !this.paused);
      }
    },
    handleNextAudio() {
      if (this.nextAudio) {
        this.$bus.$emit('next-audio');
      }
    },
    handlePreAudio() {
      this.$bus.$emit('pre-audio');
    },
  },
};
</script>

<style scoped lang="scss">
.audioControl {
  width: 210px;
  height: 80px;
  display: flex;
  .playbutton {
    width: 140px;
    height: 40px;
    display: flex;
    margin: auto;
    .play, .pause {
      margin: auto;
    }
    .pre {
      margin-top: 7.5px;
      margin-left: 0;
    }
    .next {
      margin-top: 7.5px;
      margin-right: 0;
    }
  }
}
</style>
