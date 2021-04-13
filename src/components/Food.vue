<template>
    <div>
        <h1>Name of Plate</h1>
        <img src="@/assets/redHummus.jpg" alt="">
        <p>description here with Lorem ipsum dolor sit amet consectetur adipisicing elit. Nostrum, nemo.</p>
    </div>
</template>

<script>
import {defineComponent} from 'vue'

export default defineComponent({

});
</script>

<style lang="scss">

div {
      height: 80%;

      h1 {
        font-size: 48px;
        margin-bottom: 20px;
      }
      img {
        margin-bottom: 30px;
        width: 700px;
      }
    }

</style>