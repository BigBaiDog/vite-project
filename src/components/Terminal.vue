<script setup lang="ts">
import TopBar from './TopBar.vue';
import Tset from './tset.vue';
import Executions from './Executions.vue';

</script>

<template>
    <div>
        <TopBar></TopBar>
        <!-- <Tset></Tset> -->
        <Executions></Executions>
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
</style>
