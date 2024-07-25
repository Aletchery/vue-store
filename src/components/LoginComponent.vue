<script lang="ts">
import InputText from 'primevue/inputtext'
import InputGroup from 'primevue/inputgroup'
import InputGroupAddon from 'primevue/inputgroupaddon'
import Button from 'primevue/button'
import { computed, ref } from 'vue'
import { useRouter, RouterLink } from 'vue-router'

export default {
  components: {
    InputText,
    InputGroup,
    InputGroupAddon,
    Button,
    RouterLink
  },
  setup() {
    const email = ref<string>('')
    const password = ref<string>('')
    const isDisabled = computed(() => !email.value || !password.value)
    const router = useRouter()

    const onSubmit = () => {
      console.log(email.value, password.value)
      router.push('/home')
    }

    return { email, password, isDisabled, onSubmit }
  }
}
</script>

<template>
  <form @submit.prevent="onSubmit" class="flex flex-column row-gap-4">
    <InputGroup>
      <InputGroupAddon>
        <i class="pi pi-user"></i>
      </InputGroupAddon>

      <InputText type="email" placeholder="Email" v-model="email" />
    </InputGroup>
    <InputGroup>
      <InputGroupAddon>
        <i class="pi pi-key"></i>
      </InputGroupAddon>
      <InputText type="password" placeholder="Password" v-model="password" />
    </InputGroup>
    <Button label="Login" type="submit" :disabled="isDisabled" />
  </form>
  <RouterLink to="/passreset" class="pt-3 block">Forgot your password? </RouterLink>
</template>

<style></style>
