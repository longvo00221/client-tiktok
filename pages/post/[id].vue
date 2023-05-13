<template>
  <div
    id="PostPage"
    class="fixed lg:flex justify-between z-50 top-0 left-0 w-full h-full bg-black lg:overflow-hidden overflow-auto"
  >
    <div v-if="$generalStore.selectedPost" class="lg:w-[calc(100%-540px)] h-full relative">
      <NuxtLink
      :to="$generalStore.isBackUrl"
        class="absolute z-20 m-5 rounded-full bg-gray-700 p-1.5 hover:bg-gray-800"
      >
        <Icon color="#fff" size="27" name="material-symbols:close" />
      </NuxtLink>
      <button
        class="absolute right-4 top-5 text-white bg-gray-700 font-bold py-2 px-3 rounded-xl"
      >
        Report
        <Icon name="ic:baseline-outlined-flag" />
      </button>
      <div v-if="($generalStore.ids.length > 1)" class="absolute right-4 top-[50%]">
        <button
          :disabled="!isLoaded"
          @click="($event) => loopThroughPostsUp()"
          class="flex items-center mb-5 cursor-pointer justify-center rounded-full bg-gray-700 p-1.5 hover:bg-gray-800"
        >
          <Icon name="mdi:chevron-up" size="30" color="#fff" />
        </button>
        <button
          :disabled="!isLoaded"
          @click="($event) => loopThroughPostsDown()"
          class="flex items-center cursor-pointer justify-center rounded-full bg-gray-700 p-1.5 hover:bg-gray-800"
        >
          <Icon name="mdi:chevron-down" size="30" color="#fff" />
        </button>
      </div>
      <img
        class="absolute top-[18px] left-[70px] rounded-full lg:mx-0 mx-auto"
        src="~/assets/images/tiktok-logo-small.png"
        alt="logo"
        width="45"
      />
      <!-- <video v-if="true" class="absolute object-cover w-full my-auto z-[-1] h-screen" loop autoplay controls src="/video.mp4"/> -->
      <div
        v-if="!isLoaded"
        class="flex items-center justify-center bg-black bg-opacity-70 h-screen lg:min-w-[480px]"
      >
        <Icon
          class="animate-spin ml-1"
          name="mingcute:loading-line"
          size="50"
          color="#FFFFFF"
        />
      </div>
      <div class="bg-black bg-opacity-70 lg:min-w-[480px]">
        <video
          v-if="$generalStore.selectedPost.video"
          ref="video"
          loop
          muted
          autoplay
          class="h-screen mx-auto"
          :src="$generalStore.selectedPost.video"
        />
      </div>
    </div>
    <div
      id="InfoSection"
      v-if="$generalStore.selectedPost"
      class="lg:max-w-[550px] relative w-full h-full bg-white"
    >
      <div class="py-7">
        <div class="flex items-center justify-between px-8">
          <div class="flex items-center">
            <NuxtLink :href="`/profile/${$generalStore.selectedPost.user.id}`">
              <img
               
                width="40"
                class="rounded-full object-cover lg:mx-0 mx-auto"
                alt=""
                :src="$generalStore.selectedPost.user.image"
              />
            </NuxtLink>
            <div class="ml-3 pt-0.5">
              <div class="text-[17px] font-semibold">{{ $generalStore.allLowerCaseNoCaps($generalStore.selectedPost.user.name) }}</div>
              <div class="text-[13px] -mt-5 font-light">
                {{ $generalStore.selectedPost.user.name }}
                <span class="relative -top-[2px] text-[30px] pr-0.5"> . </span>
                <span class="font-medium">{{$generalStore.selectedPost.created_at}}</span>
              </div>
            </div>
          </div>
          <Icon
            v-if="$userStore.id === $generalStore.selectedPost.user.id"
            @click="($event) => deletePost()"
            class="cursor-pointer"
            name="material-symbols:delete-outline-sharp"
            size="25"
          />
        </div>
        <div class="px-8 mt-4 text-sm">{{ $generalStore.selectedPost.text }}</div>
        <div class="px-8 mt-4 text-sm font-bold">
          <Icon name="mdi:music" size="17" />
          original sound - {{ $generalStore.selectedPost.user.name }}
        </div>
        <div class="flex items-center px-8 mt-8">
          <div class="pb-4 text-center flex items-center">
            <button
            @click="$e => isLiked ? unLikePost() : likePost()"
            class="rounded-full bg-gray-200 p-2 cursor-pointer">
              <Icon name="mdi:heart" size="25" :color="isLiked ? '#f02c56':''" />
            </button>
            <span class="text-xs pl-2 pr-4 text-gray-800 font-semibold">
              {{ $generalStore.selectedPost.likes.length }}
            </span>
          </div>
          <div class="pb-4 text-center flex items-center">
            <div class="rounded-full bg-gray-200 p-2 cursor-pointer">
              <Icon name="bx:bxs-message-rounded-dots" size="25" />
            </div>
            <span class="text-xs pl-2 pr-4 text-gray-800 font-semibold">
              123
            </span>
          </div>
        </div>
        <div
          id="Comments"
          class="bg-[#F8F8F8] z-0 w-full h-[calc(100% -273px)] border-t-2 overflow-auto"
        >
          <div class="pt-2" />
          <div v-if="false" class="text-center mt-6 text-xl text-gray-500">
            No comment
          </div>
          <div v-else class="flex items-center justify-between px-8 mt-4">
            <div class="flex items-center relative w-full">
              <NuxtLink to="/">
                <img
                  src="https://picsum.photos/id/8/300/320"
                  width="40"
                  class="absolute top-0 rounded-full lg:mx-0 mx-auto"
                  alt=""
                />
              </NuxtLink>
              <div class="ml-14 pt-0.5 w-full">
                <div
                  class="text-[18px] font-semibold flex items-center justify-between"
                >
                  User name
                  <Icon
                    v-if="true"
                    @click="($event) => deleteComment()"
                    class="cursor-pointer"
                    name="material-symbols:delete-outline-sharp"
                    size="25"
                  />
                </div>
                <div class="text-[15px] font-light">
                  Lorem ipsum dolor sit amet consectetur adipisicing elit. Natus
                  recusandae, assumenda quas nemo eveniet, necessitatibus fugit
                  quis sed facere quos sequi! Asperiores porro dolorem, expedita
                  nostrum officia ratione consectetur maxime.
                </div>
              </div>
            </div>
          </div>
          <div class="mb-28" />
        </div>
        <div
          v-if="true"
          id="CreateComment"
          class="absolute flex justify-between bottom-0 bg-white h-[85px] lg:max-w-[550px] w-full py-5 px-8 border-t-2"
        >
          <div
            :class="
              inputFocus
                ? 'border-2 border-gray-400'
                : 'border-2 border-[#f1f1f2]'
            "
            class="bg-[#f1f1f2] flex items-center rounded-lg w-full lg:max-w-[420px]"
          >
            <input
              v-model="comment"
              @focus="($event) => (inputFocus = true)"
              @blur="($event) => (inputFocus = false)"
              class="bg-[#f1f1f2] text-[14px] focus:outlint-none w-full lg:max-w-[420px] p-2 rounded-lg"
              placeholder="Add Your Comment"
              type="text"
            />
          </div>
          <button
            :disabled="!comment"
            @click="($event) => addComment()"
            :class="
              comment
                ? 'bg-[#f02c56] text-white cursor-pointer'
                : 'text-gray-400 cursor-not-allowed'
            "
            class="font-semibold text-sm ml-5 px-5 text-center rounded-lg"
          >
            Post
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const {$generalStore,$userStore,$profileStore} = useNuxtApp()
const route = useRoute();
const router = useRouter();

let inputFocus = ref(false);
let comment = ref(null);
let video = ref(null);
let isLoaded = ref(false);
onMounted(() => {
    isLoaded.value = true;
  video.value.play();
  //   video.value.addEventListener("loadeddata", (e) => {
  //     if (e.target) {
  //       setTimeout(() => {
  //         isLoaded.value = true;
  //       }, 500);
  //     }
  //   });
});
onBeforeUnmount(() => {
  video.value.pause();
  video.value.currentTime = 0;
  video.value.src = "";
});
watch(
  () => isLoaded.value,
  () => {
    if (isLoaded.value) {
      setTimeout(() => video.value.play(), 500);
    }
  }
);
</script>
