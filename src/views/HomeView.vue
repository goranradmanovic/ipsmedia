<template>
  <div class="container">
    <Header />
    <main class="main">
      <div class="main__section">
        <PageTitle />
        <Form />
      </div>
      <div class="main__slider"></div>
    </main>
  </div>
</template>

<script setup>
  import Header from '@/components/Header.vue'
  import PageTitle from '@/components/PageTitle.vue'
  import Form from '@/components/Form.vue'
</script>