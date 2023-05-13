<template>
  <div
    id="AuthOverlay"
    class="fixed transition duration-150 ease-in-out flex items-center justify-center z-50 top-0 left-0 w-full h-full bg-black bg-opacity-50"
  >
    <div 
    :class="[$generalStore.isLoginOpen === true ? 'translate-y-0' : 'translate-y-[-200%]',$generalStore.isLoginOpen === true?'opacity-100':'opacity-0' , isRegister ? 'min-h-auto' :'min-h-[80%]']"
    class="relative transition duration-150 ease-in-out bg-white w-full max-w-[470px]  h-auto p-4 rounded-lg">
      <div class="w-full flex justify-end">
        <button
        @click="$event => $generalStore.isLoginOpen = false"
        class="p-1.5 rounded-full bg-gray-100">
          <Icon name="mdi:close" size="26" />
        </button>
      </div>
      <Login v-if="isRegister"/>
      <Register v-else/>
      <div class=" bg-white flex items-center justify-center py-5 border-t w-full">
        <span class="text-[14px] text-gray-600">Don't have an account ?</span>
        <button @click="$event => isRegister = !isRegister" class="text-[14px] text-[#f02c56] font-semibold pl-1">
            <span v-if="isRegister">Sign up</span>
            <span v-else>Log in</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
const {$generalStore} = useNuxtApp()
let isRegister = ref(true)
</script>
