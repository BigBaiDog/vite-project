<script setup lang="ts">
import { ref, watchEffect, computed } from 'vue'

const { previousEvent = false } = defineProps<{
    previousEvent: boolean
}>()
const visible = ref(false)
const progress = ref('-------------------------')
const percentage = computed((): number => {
    const hashL = progress.value.split('').filter(c => c === '#').length
    return Math.floor((hashL / progress.value.length) * 100)
})
function startLoading(): Promise<void> {
    return new Promise(resolve => {
        let count: number = 0
        let rafId: number
        let step = () => {
            if (progress.value.indexOf('-') !== -1) {
                if (count % 10 === 0) {
                    progress.value = progress.value.replace('-', '#')
                }
                count++
                rafId = requestAnimationFrame(step)
            } else {
                cancelAnimationFrame(rafId)
                resolve
            }
        }
        rafId = requestAnimationFrame(step)
    })
}

watchEffect(() => {
    if (previousEvent) {
        visible.value = true
        startLoading()
    }
})
</script>

<template>
    <p v-show="visible">
        <span class="prompt">~$</span>
        <span class="progress">{{ progress }}</span>
        <span class="percentage">{{ percentage }}%</span>
    </p>
</template>

<style scoped lang="less"></style>