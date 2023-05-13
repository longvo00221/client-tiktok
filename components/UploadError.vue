<template>
  <div class="w-[100%] fixed flex justify-center">
    <div
      class="absolute  min-w-[288px] min-h-[48px] transition-all ease-in-out duration-700 top-6 z-50 mx-auto bg-black bg-opacity-70 text-white px-14 py-3 rounded-sm"
      :class="[errorType ? 'translate-y-[50px]' : 'translate-y-[-200%]',errorType?'opacity-100':'opacity-0']"
    >

{{ error }}</div>
  </div>
</template>

<script setup>
const props = defineProps(['errorType'])
const {errorType} = toRefs(props)
let error = ref('')
watch(()=>errorType.value,()=>{
    if(errorType.value == 'caption'){
        error.value = 'Maximum 150 characters'
    } else if (errorType.value == 'bio'){
        error.value = 'Maximum 80 characters'
    } else if (errorType.value == 'file'){
        error.value = 'Unsupported file Use MP4 instead'
    } else{
        error.value=''
    }
})
</script>
