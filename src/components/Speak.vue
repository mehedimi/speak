<template>
    <div class="columns">
        <div class="column is-half is-offset-one-quarter">
            <div class="box">
              <Output/>
              <Control/>
            </div>
        </div>
    </div>
</template>

<script>
import Output from './Output'
import Control from './Control'
export default {
    components: {
        Output, Control
    }
}
</script>


<style>
    #app{
        margin-top: 10px;
    }
</style>
