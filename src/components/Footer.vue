<template>
<footer>
   <div class="content">
        <h1>Remember bacalhaus</h1>
        <p>When in doubt, <b>MAKE HUMMUS!</b></p>
        <p class="disclaimer">Hummus makes no warranty that the functionality of the app will be uninterrupted or error free, that defects will be corrected or that the app or the server that makes it available are free of viruses or anything else which may be harmful or destructive.</p>
    </div>
    <img src="@/assets/brr.jpg" alt="">
</footer>
   
  
</template>

<script lang="ts">
import { defineComponent } from 'vue';
export default defineComponent({
  name: 'Footer',
});
</script>

<style lang="scss" scoped>

footer {
  display: flex;
  justify-content: space-around;
  align-items: center;

  .content {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    width: 60%;

    h1 {
      font-size: 48px;
      width: 60%;
      text-align: left;
    }

    p {
      font-size: 22px;
      width: 60%;
      margin: 10px 0 10px 0;
    }

    .disclaimer {
      color: #7a7878;
      font-size: 14px;
    }
    
  }

  img {
    width: 50%;
  }
}
</style>