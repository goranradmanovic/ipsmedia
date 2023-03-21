<template>
  <form class="form">
    <div class="form__group">
      <img src="@/assets/icons/mail-icon.svg" alt="Envelop image" class="form__group__img" />
      <input
        type="email"
        id="email"
        v-model="emailInput"
        class="form__group__input"
        :class="{ error: v$.emailInput.$errors.length > 0 }"
      />
      <label
        for="email"
        class="form__group__label"
        :class="{ error: v$.emailInput.$errors.length > 0, focus: emailInput !== '' }"
      >
        <span v-if="v$.emailInput.$errors.length > 0">
          <span v-for="error in v$.emailInput.$errors" :key="error.$uid">
            {{ error.$message }}
          </span>
        </span>
        <span v-else>Enter your Email Address</span>
      </label>
    </div>

    <Button class="form__btn" @click.prevent="submitForm()">Please notify me</Button>
  </form>
</template>

<script setup>
import { ref } from 'vue'
import { useVuelidate } from '@vuelidate/core'
import { required, email, helpers } from '@vuelidate/validators'
import { useRouter } from 'vue-router'
import Button from '@/components/Button.vue'

const emailInput = ref(''),
  router = useRouter(),
  rules = {
    emailInput: {
      required: helpers.withMessage('Email is required', required),
      email: helpers.withMessage('Please enter a valid email', email)
    }
  },
  v$ = useVuelidate(rules, { emailInput })

const submitForm = async () => {
  const result = await v$.value.$validate() // true/false

  if (result) {
    // Redirect
    router.push({ name: 'thankyou' })
  }

  return
}
</script>
