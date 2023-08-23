<script setup lang="ts">
import { ref, Ref, watch } from 'vue';

const randomNumeric: Ref<number> = ref(0);
const minRange: Ref<number> = ref(1);
const maxRange: Ref<number> = ref(100);
const intervalId: Ref<number> = ref(0);
const isGenerateBtnDisabled: Ref<boolean> = ref(false)

const getRandomNumeric: () => void = () => {
  isGenerateBtnDisabled.value = true
  const localMin = Math.ceil(minRange.value),
    localMax = Math.floor(maxRange.value)

  intervalId.value = setInterval(() => {
    randomNumeric.value =
      Math.floor(Math.random() * (localMax - localMin + 1)) + localMin;
  }, 500);
};


watch(intervalId, () => {
  setTimeout(() => {
    clearTimeout(intervalId.value);
    isGenerateBtnDisabled.value = false
  }, 2000);
});
</script>

<template>
  <main class="container mx-auto my-12 px-3 text-center">
    <div class="bg-white bg-opacity-70 rounded-xl p-10 border-solid border-2 border-emerald-600">
      <div class="w-full grid grid-cols-2 gap-4">
        <div class="p-7">
          <h2 class="text-5xl mb-5 font-mono text-cyan-900">
            Numeric randomize
          </h2>
          <div class="flex-col mb-4">
            <p class="text-2xl font-mono text-cyan-900 mb-3">Min</p>
            <input v-model="minRange" class="w-3/4 h-10 px-3 py-2" placeholder="min" type="text" />
          </div>
          <div class="flex-col mb-16">
            <p class="text-2xl font-mono text-cyan-900 mb-3">Max</p>
            <input v-model="maxRange" class="w-3/4 h-10 px-3 py-2" placeholder="max" type="text" />
          </div>
          <button @click="getRandomNumeric" :disabled='isGenerateBtnDisabled'
            class="w-3/4 px-4 py-2 rounded-md bg-emerald-600 text-white text-2xl">
            Generate
          </button>
        </div>
        <div class="p-7">
          <div class="grid grid-cols-2 gap-2 mb-9">
            <div class="">
              <h3 class="text-4xl text-cyan-900 font-mono mb-2">Min Range</h3>
              <p class="text-2xl text-cyan-900 font-mono">{{ minRange }}</p>
            </div>
            <div class="">
              <h3 class="text-4xl text-cyan-900 font-mono mb-2">Max Range</h3>
              <p class="text-2xl text-cyan-900 font-mono">{{ maxRange }}</p>
            </div>
          </div>
          <div class="w-full flex justify-center items-center h-64 border-solid border-cyan-400 border-2">
            <h5 class="text-8xl text-cyan-900 font-mono">
              {{ randomNumeric }}
            </h5>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style lang="scss" scoped></style>
