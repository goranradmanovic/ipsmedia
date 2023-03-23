<template>
  <div class="container">
    <main class="main">
      <div class="main__section">
        <PageTitle />
        <Form />
      </div>
      <div class="main__slider">
        <Slider />
      </div>
    </main>
  </div>
</template>

<script setup>
import PageTitle from '@/components/PageTitle.vue'
import Form from '@/components/Form.vue'
import Slider from '@/components/Slider.vue'
</script>
