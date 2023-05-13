<template>
  <NuxtPage/>
  <AuthOverlay v-if="isLoginOpen"/>
  <EditProfileOverlay v-if="isEditProfileOpen" />
</template>

<script setup>
import { storeToRefs } from 'pinia';
const {$generalStore,$userStore} = useNuxtApp()
const {isLoginOpen , isEditProfileOpen} = storeToRefs($generalStore)
onMounted(async ()=>{
  $generalStore.bodySwitch(false)
  try {
    await $generalStore.getRandomUsers('suggested')
    await $generalStore.getRandomUsers('following')
    await $generalStore.hasSessionExpired()
    if($userStore.id){
      $userStore.getUser()
    }
  } catch (error) {
    console.log(error)
  }
})
watch(()=>isLoginOpen.value,(val) => $generalStore.bodySwitch(val))
watch(()=>isEditProfileOpen.value,(val) => $generalStore.bodySwitch(val))
</script>