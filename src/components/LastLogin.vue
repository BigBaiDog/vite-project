<script setup lang="ts">
import { ref,watchEffect } from 'vue'

const emit = defineEmits(['complete'])
const { previousEvent = false } = defineProps<{
    previousEvent: boolean
}>()

const date = (new Date()).toDateString()
const ip = location.host
const connected = ref(false)

watchEffect(async () => {
    if (previousEvent) {
        connected.value = true
        emit('complete')
    }
})
</script>

<template>
    <p v-if="connected">Last login: {{ date }} from {{ ip }}</p>
    <p v-else>Connecting ...</p>
</template>

<style lang="less"></style>