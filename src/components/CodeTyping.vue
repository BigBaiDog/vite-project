<script setup lang="ts">
import { ref, computed, watchEffect } from 'vue'
import Prism from "prismjs"
import 'prismjs/themes/prism-tomorrow.css'
// import 'prismjs/themes/prism-okaidia.css'
import '@fontsource-variable/jetbrains-mono'
import data from '../assets/data'

const emit = defineEmits(['complete'])
const { previousEvent = false } = defineProps<{
    previousEvent: boolean
}>()
const currentCode = ref('')
const isCursorVisible = ref('none')
const codeWithCursor = computed(() => {
    let highlightedCode = Prism.highlight(
        currentCode.value,
        Prism.languages.javascript
    )
    return `${highlightedCode}<span class="cursor" style="display:${isCursorVisible.value}">▌</span>`
})
function typingAnimation(codeContent: string): Promise<void> {
    return new Promise((resolve) => {
        let count = 0, typingCount = 0
        let step = () => {
            let randomNumber = Math.round(Math.random() * 6)
            if (count % 2 === 0 && randomNumber % 6 === 0) {
                currentCode.value = codeContent.substring(0, typingCount++)
            }
            count++
            if (typingCount <= codeContent.length) {
                requestAnimationFrame(step)
            } else {
                resolve()
            }
        }
        requestAnimationFrame(step)
    })
}

watchEffect(async () => {
    if (previousEvent) {
        isCursorVisible.value = 'line'
        await typingAnimation(data.code as string)
        isCursorVisible.value = 'none'
        emit('complete')
    }
})
</script>

<template>
    <pre>
        <code v-html="codeWithCursor"></code>
     </pre>
</template>

<style lang="less">
.cursor {
    color: #BBB;
    animation: blink 500ms step-end infinite;
}

@keyframes blink {
    50% {
        opacity: 0;
    }
}
</style>