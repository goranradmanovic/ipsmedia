<template>
  <div class="thankyou">
    <div class="thankyou__wrapper">
      <h1 class="thankyou__title">Thank You!</h1>
      <p class="thankyou__text">You will get notified when iPhone Photo Academy becomes available</p>
      <div class="thankyou__btn" @click="redirect()">
        <span class="thankyou__btn_text">Subscribe To Our Youtube Channel</span>
      </div>
    </div>
  </div>
</template>

<script setup>
  const redirect = () => {
    window.open('https://www.youtube.com/user/iPhonePS?sub_confirmation=1', '_blank')
  }
</script>
