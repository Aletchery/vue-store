<script lang="ts">
import InputText from 'primevue/inputtext'
import InputGroup from 'primevue/inputgroup'
import InputGroupAddon from 'primevue/inputgroupaddon'
import Button from 'primevue/button'
import { computed, ref } from 'vue'
import { useRouter } from 'vue-router'

export default {
  components: {
    InputText,
    InputGroup,
    InputGroupAddon,
    Button
  },
  setup() {
    const email = ref<string>('')
    const password1 = ref<string>('')
    const password2 = ref<string>('')
    const isDisabled = computed(
      () =>
        !email.value || !password1.value || !password2.value || password1.value !== password2.value
    )

    const router = useRouter()

    const onSubmit = () => {
      console.log(email.value, password1.value)
      router.push('/')
    }

    return { email, password1, password2, isDisabled, onSubmit }
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
      <InputText type="password" placeholder="Password" v-model="password1" />
    </InputGroup>
    <InputGroup>
      <InputGroupAddon>
        <i class="pi pi-key"></i>
      </InputGroupAddon>
      <InputText type="password" placeholder="Password" v-model="password2" />
    </InputGroup>
    <Button label="Reset password" type="submit" :disabled="isDisabled" />
  </form>
</template>

<style></style>
