<script setup lang="ts">
import { ref, watchEffect, defineEmits } from 'vue'
import data from '../assets/data'

const emit = defineEmits(['complete'])
const { previousEvent = false } = defineProps<{
    previousEvent: boolean
}>()
class Execution {
    visible: boolean = false
    time: string = ''
    name: string
    duration: number = 0
    constructor(name: string) {
        this.name = name
    }
    getRandomNumber(): number {
        const randomNumber = Math.random() * (500 - 300) + 300
        return parseFloat(randomNumber.toFixed(2))
    }
    run(): Promise<void> {
        return new Promise((resolve) => {
            this.time = new Date().toLocaleTimeString()
            this.duration = this.getRandomNumber()
            setTimeout(() => {
                this.visible = true
                resolve()
            }, this.duration)
        })
    }
}
const executions = ref<Execution[]>([]);
(data.executions as Array<{ name: string }>).forEach((execution) => {
    executions.value.push(new Execution(execution.name))
})

watchEffect(async () => {
    if (previousEvent) {
        await executions.value[0].run()
        await executions.value[1].run()
        await executions.value[2].run()
        emit('complete')
    }
})
</script>

<template>
    <p v-for="job in executions" v-show="job.visible">
        <span class="prompt">~$</span>
        <span class="time">[{{ job.time }}]</span>
        <span class="task">{{ job.name }}</span>
        <span class="duration">{{ job.duration }}ms</span>
    </p>
</template>

<style scoped lang="less"></style>