<template>
  <div id="home">
    <fancy-image
      :src="`https://images.unsplash.com/photo-1682687982360-3fbab65f9d50?q=80&w=2940&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&cb=${cb}`"
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
