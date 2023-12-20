<template>
    <canvas ref="canvas" :width="width" :height="height"></canvas>
</template>

<script>
    import { decode } from "blurhash";

    export default {
        name: 'VueBlurHash',
        props: {
            hash: {
                type: String,
                required: true
            },
            width: {
                type: Number,
                required: true
            },
            height: {
                type: Number,
                required: true
            }
        },
        data() {
            return {
                rendered: false
            }
        },
        mounted() {
            const pixels = decode(this.hash, this.width, this.height)
            const ctx = this.$refs.canvas.getContext("2d")
            const imageData = ctx.createImageData(this.width, this.height)
            imageData.data.set(pixels)
            ctx.putImageData(imageData, 0, 0)
            this.rendered = true
            this.$emit('rendered')
        }
    }
</script>
