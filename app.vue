<script setup>
import { onMounted } from 'vue'
import { useUserStore } from '@/stores/user'

const userStore = useUserStore()

onMounted(() => {
  userStore.initStore()
})
</script>

<template>
  <div>
    <NuxtLayout><!--For wrapping common layout elements-->
      <NuxtPage/><!--This is the main content-->
    </NuxtLayout>
  </div>
</template>
