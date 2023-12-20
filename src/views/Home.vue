<template>
  <div id="home">
    <fancy-image
      :src="`https://raw.githubusercontent.com/lukaswhite/vue-blurhash-demo/main/assets/photo.jpg?cb=${cb}`"
      blurhash="LuBqYz%0MxRQ*0tQRPRk%Mt7R.WY"/>
  </div>
</template>

<script>

  function makeid(length) {
    let result = '';
    const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
    const charactersLength = characters.length;
    let counter = 0;
    while (counter < length) {
      result += characters.charAt(Math.floor(Math.random() * charactersLength));
      counter += 1;
    }
    return result;
  }


  import FancyImage from "../components/FancyImage";
  export default {
    components: {FancyImage},
    computed:{
      cb(){
        return makeid(32)
      }
    }
  }

</script>
