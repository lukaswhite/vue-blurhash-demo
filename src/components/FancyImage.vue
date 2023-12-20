<template>
    <figure ref="container" v-aspect-ratio="'4:3'">
        <img width="600" key="image" :src="src" @load="loaded = true" v-show="loaded" />
        <vue-blur-hash key="loading" :width="600" :height="400" :hash="blurhash" :class="{'hidden':loaded}" />
    </figure>
</template>

<script>
    import { directive } from 'v-aspect-ratio'
    import VueBlurHash from "./VueBlurHash";

    export default {
        name: "FancyImage",
        components: {VueBlurHash},
        directives: {
            'aspect-ratio': directive,
        },
        props:{
            src:{
                type:String,
                required:true
            },
            blurhash:{
                type:String,
                required:true
            }
        },
        data:()=>{
            return {
                loaded: false
            }
        }
    }
</script>

<style scoped>
    .fade-enter-active, .fade-leave-active {
        transition: opacity .2s
    }
    .fade-enter, .fade-leave-to {
        opacity: 0
    }
    .hidden {
        opacity: 0;
        transition: opacity 1s;
    }
    img.hidden {
        transition-delay: 1s;
    }
    img {
        max-width: 100%;
    }
    figure {
        position: relative;
    }
    canvas, img {
        position: absolute;
    }
</style>
