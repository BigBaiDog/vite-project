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
    <p v-if="connected"><span>Last login: </span><span>{{ date }} </span><span>from </span><span>{{ ip }}</span></p>
    <p v-else><span>Connecting ...</span></p>
</template>

<style lang="less"></style>