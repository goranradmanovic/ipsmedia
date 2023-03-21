<template>
  <div class="thankyou">
    <div class="thankyou__wrapper">
      <h1 class="thankyou__title">Thank You!</h1>
      <p class="thankyou__text">You will get notified when iPhone Photo Academy becomes available</p>
      <Button class="thankyou__btn" @click="redirect()">Subscribe To Our Youtube Channel</Button>
    </div>
  </div>
</template>

<script setup>
  import Button from '@/components/Button.vue'

  const redirect = () => {
    window.open('https://www.youtube.com/user/iPhonePS?sub_confirmation=1', '_blank')
  }
</script>
