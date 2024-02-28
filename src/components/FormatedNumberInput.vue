<script setup lang="ts">
import { ref, computed } from 'vue'
const props = defineProps(['modelValue'])
const emit = defineEmits(['update:modelValue'])

const myValue = ref(props.modelValue)

const inputWidth = computed(() => {
    if (myValue.value === null) {
        return 0
    } else {
        return document.getElementById('scale')?.offsetWidth || 0
    }
})

const inputHandler = (event: Event) => {
    const target = event.target as HTMLInputElement
    //console.log(`target.value : ${target.value}`)
    // On enlève les caractères non numériques
    const integerValue = target.value.replace(/\D/g, '')
    // On ajoute des espace pour les séparer les milliers
    const numberValue = Number.parseInt(integerValue) || null
    //console.log(`numberValue : ${numberValue}`)
    const formatedValue = numberValue?.toLocaleString('fr-fr', { useGrouping: true }) || null
    //console.log(`formatedValue : ${formatedValue}`)
    myValue.value = formatedValue
    target.value = formatedValue
    emit('update:modelValue', numberValue)
}
</script>

<template>
    <input
            :value="myValue"
            @input="inputHandler"
            name="hours-old"
            id="hours-old"
            class="border-gray-300 border rounded p-1"
            :class="{'border-purple-500': myValue !== null, 'border-[2px]': myValue !== null}"
            :style="{ width: inputWidth + 'px'}"
          />
    <span class="invisible absolute" id="scale">{{ myValue }}</span>
</template>

<style>
#hours-old {
    min-width: 72px;
}
</style>
