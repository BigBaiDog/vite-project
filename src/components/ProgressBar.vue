<script setup lang="ts">
import {onMounted ,computed,ref} from 'vue';

let progress=ref('-------------------------');

const percentage = computed(() => {
    const hashL = progress.value.split('').filter(c => c === '#').length;
    return Math.floor((hashL / progress.value.length) * 100);
});

function startLoading(): Promise<void> {
    return new Promise((resolve) => {
        let count: number= 0;
        let rafId :number
        const step = () => {
            if (progress.value.indexOf('-') === -1) {
                cancelAnimationFrame(rafId);
                resolve();
            } else {
                if (count % 3 === 0) {
                    progress.value = progress.value.replace('-', '#');
                }
                count++;
                rafId = requestAnimationFrame(step);
            }
        };
        rafId = requestAnimationFrame(step);
    });
}

onMounted(async () => {
    await startLoading();
});
</script>

<template>
    <p class="code">
        <span class="prompt">~$</span>
        <span class="">{{ progress }}</span>
        <span class="percentage">{{ percentage }}%</span>
    </p>
</template>

<style scoped lang="less">

</style>