<template>
    <div class="field">
        <div class="control">
            <textarea v-model="output" class="textarea is-primary" type="text" placeholder="Speak to me"></textarea>
        </div>
    </div>
</template>

<script>
import Bus from '../helpers/bus'

export default {
    data(){
        return {
            output: ''
        }
    },
    mounted: function () {
        Bus.$on('finish-speak', (text) => {
            this.showOutput(text)
        })
        Bus.$on('clear-message', () => {
            this.output = ''
        })
        Bus.$on('listen-stop', () => {
            this.speakBack()
        })
    },
    methods: {
        showOutput(text){
            this.output += ' ' + text;
        },
        speakBack(){
            let speaker = new SpeechSynthesisUtterance()
            speaker.text = 'You said to me.'+this.output
            window.speechSynthesis.speak(speaker)
            speaker = null
        }
    }
}
</script>

<style>

</style>
