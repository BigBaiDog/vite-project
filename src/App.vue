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
// div {
//     position: fixed;
//     top: 0;
//     left: 0;
//     width: 100%;
//     height: 100%;
//     // background: #263238;
// }

// .code {
//     color: #BBB;
//     font-family: 'JetBrains Mono Variable', monospace;
//     // line-height: 1.2;
//     // text-shadow: 1px 1px 5px;
//     // font-family: 'Roboto Mono', 'Menlo', 'Monaco', Courier, monospace !important;
//     // font-weight: 500 !important;
//     // font-size: 16px ;
// <!-- } -->
</style>