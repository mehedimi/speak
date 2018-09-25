<template>
  <div id="app">
    <Speak v-if="isSupported()"/>
    <div v-else class="is-center">
      <h1>Your browser doesn't support this App</h1>
    </div>
  </div>
</template>

<script>
import Speak from './components/Speak'

export default {
    name: "app",
    components: {
      Speak      
    },
    methods: {
      isSupported(){
        return (window.SpeechRecognition || window.webkitSpeechRecognition)
      }
    }
};
</script>

<style lang="sass">
  @import 'bulma';
</style>
