<script setup lang="ts">
import { ref, onMounted } from 'vue'
import TopBar from './components/TopBar.vue'
import LastLogin from './components/LastLogin.vue'
import CodeTyping from './components/CodeTyping.vue'
import Executions from './components/Executions.vue'
import ProgressBar from './components/ProgressBar.vue'
import '@fontsource-variable/jetbrains-mono'

const completed = ref({
    login: false,
    typing: false,
    execution: false
})
const begin = ref(false)

onMounted(() => {
    setTimeout(() => {
        begin.value = true
    }, 500)
})
</script>

<template>
    <TopBar></TopBar>
    <LastLogin :previousEvent="begin" @complete="completed.login = true"></LastLogin>
    <CodeTyping :previousEvent=completed.login @complete="completed.typing = true"></CodeTyping>
    <Executions :previousEvent=completed.typing @complete="completed.execution = true"></Executions>
    <ProgressBar :previousEvent="completed.execution"></ProgressBar>
</template>

<style scoped lang="less">
</style>