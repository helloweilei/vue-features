<!-- eslint-disable @typescript-eslint/no-explicit-any -->
<script setup lang="ts">
import { ref } from 'vue'
import DemoBlock from './DemoBlock.vue'

// 自定义指令：文本高亮
const vHighlight = {
    mounted(el: HTMLElement) {
        el.style.backgroundColor = 'yellow'
        el.style.padding = '2px 6px'
        el.style.borderRadius = '4px'
    },
}

const highlightCode = `const vHighlight = {
    mounted(el: HTMLElement) {
        el.style.backgroundColor = 'yellow'
        el.style.padding = '2px 6px'
        el.style.borderRadius = '4px'
    },
}`

// 自定义指令：聚焦
const vFocus = {
    mounted(el: HTMLElement) {
        ; (el as HTMLInputElement).focus()
    },
}

// 自定义指令：点击外部关闭
const vClickOutside = {
    mounted(el: HTMLElement, binding: { value: (e: Event) => void }) {
        (el as any).clickOutsideEvent = function (event: MouseEvent) {
            if (!(el as any).contains(event.target)) {
                binding.value(event)
            }
        }
        setTimeout(() => {
            document.addEventListener('click', (el as any).clickOutsideEvent)
        }, 0)
    },
    unmounted(el: HTMLElement) {
        document.removeEventListener('click', (el as any).clickOutsideEvent)
    },
}

const show = ref(false)
const clickOutsideCode = `
{
    mounted(el: HTMLElement, binding: { value: (e: Event) => void }) {
        (el as any).clickOutsideEvent = function (event: MouseEvent) {
            if (!(el as any).contains(event.target)) {
                binding.value(event)
            }
        }
        document.addEventListener('click', (el as any).clickOutsideEvent)
    },
    unmounted(el: HTMLElement) {
        document.removeEventListener('click', (el as any).clickOutsideEvent)
    },
}`

</script>

<template>
    <div class="directives-demo">
        <!-- Highlight Directive Demo -->
        <div class="demo-item">
            <DemoBlock title="文本高亮指令" :code="highlightCode">
                <div>
                    <h4>v-highlight: 文本高亮指令</h4>
                    <p>
                        这是一个
                        <span v-highlight>高亮文本</span>
                        ，使用自定义指令实现。
                    </p>
                </div>
            </DemoBlock>
            <DemoBlock title="聚焦指令" description="自定义指令用于聚焦元素" :code="`const vFocus = {
    mounted(el: HTMLElement) { (el as HTMLInputElement).focus() }},`">
                <div>
                    <h4>v-focus: 聚焦指令</h4>
                    <input type="text" placeholder="请输入内容" v-focus />
                </div>
            </DemoBlock>
            <DemoBlock title="点击外部关闭指令" description="自定义指令用于点击外部关闭元素" :code="clickOutsideCode">
                <div>
                    <h4>v-click-outside: 点击外部关闭指令</h4>
                    <button @click="show = true">点击打开</button>
                    <div v-if="show" class="click-outside-box" v-click-outside="() => show = false">
                        <p>点击外部关闭</p>
                        <button @click="show = false">点击关闭</button>
                    </div>
                </div>
            </DemoBlock>
        </div>
    </div>
</template>

<style scoped>
.directives-demo {
    padding: 20px;
}

.demo-item {
    margin-bottom: 24px;
    padding: 0px 16px 0px 16px;
    background-color: #f9fafb;
    border-radius: 6px;
    border-left: 4px solid #3b82f6;
}

.demo-item h4 {
    margin: 0 0 12px 0;
    font-size: 14px;
    font-weight: 600;
    color: #1f2937;
}

.demo-item p {
    margin: 0;
    font-size: 14px;
    color: #4b5563;
}

input {
    padding: 6px 12px;
    border: 1px solid #d1d5db;
    border-radius: 4px;
    font-size: 14px;
}

input:focus {
    outline: none;
    border-color: #3b82f6;
    box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
}

button {
    padding: 6px 16px;
    background-color: #3b82f6;
    color: white;
    border: none;
    border-radius: 4px;
    font-size: 14px;
    cursor: pointer;
    transition: background-color 0.2s;
}

button:hover {
    background-color: #2563eb;
}

.click-outside-box {
    display: inline-block;
    padding: 12px 16px;
    background-color: #fff3cd;
    border: 1px solid #ffc107;
    border-radius: 4px;
    color: #664d03;
}

.click-outside-box.hidden {
    display: none;
}

.click-outside-box p {
    margin: 0 0 8px 0;
    color: #664d03;
}
</style>
