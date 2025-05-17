<script setup lang="ts">
import {ref, computed, onMounted } from 'vue';
import Prism from "prismjs";
import 'prismjs/themes/prism-tomorrow.css'
// import 'prismjs/themes/prism-okaidia.css'
import '@fontsource-variable/jetbrains-mono';
import data from '../assets/data';

const date = (new Date()).toDateString()
const ip = location.hostname
const currentCode = ref('')
const codeWithCursor = computed(() => {
    let highlightedCode = Prism.highlight(
            currentCode.value,
            Prism.languages.javascript
        )
        var a = 'Last login: ' + date + ' from '+ip+''
        var b = Prism.highlight(
            a,
            Prism.languages.javascript
        )
        return  b+highlightedCode + '<span class="cursor">▌</span>'
    })
function typingAnimation(codeContent: string): Promise<void> {
    return new Promise((resolve) => {
        let count = 0, typingCount = 0
        let step = () => {
            let randomNumber = Math.round(Math.random() * 6)
            if (count % 2 === 0 && randomNumber % 1 === 0) {
                currentCode.value = codeContent.substring(0, typingCount++);
            }
            count++
            if (typingCount <= codeContent.length) {
                requestAnimationFrame(step)
            } else {
                resolve()
            }
        };
        requestAnimationFrame(step)
    })
}

onMounted(() => {
    typingAnimation(data.code as string)
})

</script>

<template>
    <!-- <p class="code">Last login: {{ date }} from {{ ip }}</p> -->
     <pre>
        <code class="code" style="text-align: left" v-html="codeWithCursor"></code>
     </pre>
    
</template>

<style lang="less">
code {
    color: #BBB;
    font-family: 'JetBrains Mono Variable', monospace;
    // line-height: 1.2;
    // text-shadow: 1px 1px 5px;
    // font-family: 'Roboto Mono', 'Menlo', 'Monaco', Courier, monospace !important;
    // font-weight: 500 !important;
    // font-size: 16px ;
}

.cursor {
    color: #BBB;
    animation: blink 1s step-end infinite;
    /* 动画名称 持续时间 无限次循环 */
}

@keyframes blink {

    /* 0%, 100% { opacity: 1; } 完全不透明 */
    50% {
        opacity: 0;
    }

    /* 完全透明 */
}
</style>