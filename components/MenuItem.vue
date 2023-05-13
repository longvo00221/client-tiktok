<template>
  <div
    class="w-full flex items-center hover:bg-gray-100 p-2.5 rounded-md cursor-pointer"
  >
    <div class="flex items-center lg:mx-0 mx-auto">
      <Icon :name="icon" :color="colorString" :size="sizeString" />
      <div class="flex items-center">
        <span
          :class="`text-[${colorString}]`"
          class="lg:block hidden pl-[9px] mt-0.5 font-bold text-[17px]"
          >{{ iconString }}</span
        >

        <span
          v-if="iconString === 'Explore'"
          class="px-2 ml-2 hidden lg:block rounded-full bg-[#fe2c55] font-semibold text-white text-sm"
          >New</span
        >
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps(["iconString", "colorString", "sizeString"]);
const { iconString, colorString, sizeString } = toRefs(props);

let icon = ref("");
if (iconString.value === "For You") icon.value = "mdi:home";
if (iconString.value === "Following") icon.value = "ci:group";
if (iconString.value === "Explore") icon.value = "carbon:explore";
if (iconString.value === "LIVE") icon.value = "ri:live-line";
</script>
