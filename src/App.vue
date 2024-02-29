<template>
  <div class="max-w-lg mx-auto py-20">
    <div class="flex items-center gap-3">
      <div class="bg-white rounded-full w-[88px] h-[88px] p-1 shrink-0" :class="{'inner-border': student.age != null}">
        <img :src="student.image || ''" class="bg-gray-300 w-full h-full object-cover rounded-full" />
      </div>
      <div>
        <label for="hours-old" class="koulen-regular" :class="{'text-[#3D06D7]': student.age != null}">{{ student.name }} is</label>
        <div class="flex items-center gap-3 mt-3">
          <FormatedNumberInput v-model="student.age" />
          <div class="text inter-400 h-fit">hours old</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, ref } from 'vue'
import FormatedNumberInput from './components/FormatedNumberInput.vue'

const student = reactive<{
  name: string
  age: number | null
  image: string | null
}>({
  name: 'Samuel',
  age: null,
  image: '/photo.jpg',
})
</script>

<style>
.inner-border {
  -webkit-box-shadow:inset 0px 0px 0px 1px #3D06D7;
  -moz-box-shadow:inset 0px 0px 0px 1px #3D06D7;
  box-shadow: inset 0px 0px 0px 1px #3D06D7;
}
</style>
