<script setup lang="ts">
</script>

<template>
    <header class="top-bar">
        <a href="javascript:;" class="close"></a>
        <a href="javascript:;" class="minimize"></a>
        <a href="javascript:;" class="maximize"></a>
    </header>
</template>

<style scoped lang="less">
header {
    // position: absolute;
    // top: 0;
    // left: 0;
    width: 100%;
    height: 16px;
    padding: 16px;

    >a {
        float: left;
        display: block;
        width: 16px;
        height: 16px;
        margin-right: 8px;
        border-radius: 8px;

        &.close {
            background-color: #FF5F56;
        }

        &.minimize {
            background-color: #FFBD2E;
        }

        &.maximize {
            background-color: #27C93F;
        }

    }
}
</style>