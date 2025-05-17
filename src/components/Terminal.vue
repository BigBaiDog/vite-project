<script setup lang="ts">
import TopBar from './TopBar.vue';
import Tset from './tset.vue';
import Executions from './Executions.vue';
import ProgressBar from './ProgressBar.vue';

import '@fontsource-variable/jetbrains-mono';
</script>

<template>
    <div>
        <TopBar></TopBar>
        <!-- <Tset></Tset> -->
        <!-- <Executions></Executions> -->
        <ProgressBar></ProgressBar>
    </div>
</template>

<style scoped lang="less">
div {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    // background: #263238;
}
.code {
    color: #BBB;
    font-family: 'JetBrains Mono Variable', monospace;
    // line-height: 1.2;
    // text-shadow: 1px 1px 5px;
    // font-family: 'Roboto Mono', 'Menlo', 'Monaco', Courier, monospace !important;
    // font-weight: 500 !important;
    // font-size: 16px ;
}
</style>
