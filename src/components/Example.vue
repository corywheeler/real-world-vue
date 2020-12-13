<template>
  <form @submit.prevent="submit">
    <input
      :class="{ error: $v.email.$error }"
      type="email"
      placeholder="What's your email"
      v-model="email"
      @blur="$v.email.$touch()"
    />
    <div v-if="$v.email.$error">
      <p class="errorMessage" v-if="!$v.email.email">
        Please enter in a valid email
      </p>
      <p class="errorMessage" v-if="!$v.email.required">
        Email is required
      </p>
    </div>
    <button :disabled="$v.$invalid" type="submit">Submit</button>
    <p v-if="$v.$anyError" class="errorMessage">
      Please fill out the required fields
    </p>
  </form>
</template>

<script>
import { required, email } from 'vuelidate/lib/validators'

export default {
  name: 'Example',
  data() {
    return {
      email: null
    }
  },
  validations: {
    email: {
      required,
      email
    }
  },
  methods: {
    submit() {
      this.$v.$touch()

      if (!this.$v.$invalid) {
        console.log('Form submitted:', this.email)
      }
    }
  }
}
</script>

<style scoped></style>
