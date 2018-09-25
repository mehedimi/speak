<template>
  <div class="field is-grouped">
    <p class="control">
      <button class="button is-danger" @click="stopSpeaking">Stop Speaking</button>
    </p>
    <p class="control">
      <button @click="startSpeaking" class="button is-primary" :class="{'is-loading': isSpeaking}">Start Speaking</button>
    </p>
    <p class="control">
      <button class="button is-info" @click="clearMessage">Clear</button>
    </p>
  </div>
</template>

<script>
import Bus from '../helpers/bus'
export default {
  data(){
    return {
      isSpeaking: false,
      recognizer: null
    }
  },
  mounted(){
    let recognizer = this.recognizerInstance()
    recognizer.onresult = (e) => {
      Bus.$emit('finish-speak', e.results[0][0].transcript)
    }
    recognizer.onspeechend = () => {
      this.stopSpeaking()
    }
    recognizer.onend = () => {
      Bus.$emit('listen-stop')
    }
    this.recognizer = recognizer
  },
  methods: {
    startSpeaking(){
      this.isSpeaking = true
      this.recognizer.start()
    },
    stopSpeaking(){
      this.isSpeaking = false
      this.recognizer.stop()
    },
    recognizerInstance(){
      if (window.SpeechRecognition) {
        // eslint-disable-next-line
        return new SpeechRecognition()
      }
      // eslint-disable-next-line
      return new webkitSpeechRecognition()
    },
    clearMessage(){
      Bus.$emit('clear-message')
    }
  }
};
</script>

<style>
</style>
