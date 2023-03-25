<template>
  <div class="container">
    <main class="main">
      <div class="main__section">
        <Content />
        <Form />
      </div>
      <div class="main__slider">
        <Slider />
      </div>
    </main>
  </div>
</template>

<script setup>
import Content from '@/components/Content.vue'
import Form from '@/components/Form.vue'
import Slider from '@/components/Slider.vue'
</script>
