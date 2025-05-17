<script setup lang="ts">
import data from '../assets/data';
import { onMounted, ref } from 'vue';

class Execution {
    visible: boolean = false;
    time: string = '';
    name: string;
    duration: number = 0;
    constructor(name: string, duration?: number) {
        this.name = name;
        if (duration !== undefined) {
            this.duration = duration;
        }
    }
    getRandomNumber(): number {
        const randomNumber = Math.random() * (500 - 300) + 300; // 生成200到300之间的随机数
        return parseFloat(randomNumber.toFixed(2)); // 精确到小数点后两位
    }
    run(): Promise<void> {
        return new Promise((resolve) => {
            this.time = new Date().toLocaleTimeString();
            this.duration = this.getRandomNumber();
            setTimeout(() => {
                this.visible = true;
                resolve();
            }, this.duration);
        });
    }
}

const executions = ref<Execution[]>([]);
(data.executions as Array<{ name: string }>).forEach((execution) => {
    executions.value.push(new Execution(execution.name));
});

onMounted(async () => {
    await executions.value[0].run();
    await executions.value[1].run();
    await executions.value[2].run();

});

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