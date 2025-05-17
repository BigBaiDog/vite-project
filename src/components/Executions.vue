<script setup lang="ts">
import date from '../assets/data';  
function executeACommand(execution :object) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(execution.result);
        }, execution.duration);
    });
}

</script>

<template>
    <span class="prompt">~$ </span>
    <span class="time">[时间] </span>
    <span class="task">运行中 </span>
    <span class="duration">200ms</span>
</template>

<style scoped lang="less">

</style>
