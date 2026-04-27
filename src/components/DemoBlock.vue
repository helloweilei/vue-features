<script setup lang="ts">
import { ref, onUpdated } from 'vue'
import hljs from 'highlight.js'
import 'highlight.js/styles/atom-one-dark.css'

interface Props {
    title: string
    description?: string
    code?: string
}

defineProps<Props>()

const showCode = ref(false)
const codeEl = ref<HTMLElement | null>(null)

onUpdated(() => {
    if (showCode.value && codeEl.value) {
        hljs.highlightElement(codeEl.value as HTMLElement)
    }
})
</script>

<template>
    <div class="demo-block">
        <div class="demo-block-header">
            <h3 class="demo-block-title">{{ title }}</h3>
            <p v-if="description" class="demo-block-description">{{ description }}</p>
        </div>

        <!-- Demo Preview Area -->
        <div class="demo-block-preview">
            <slot />
        </div>

        <!-- Code Toolbar -->
        <div class="demo-block-toolbar">
            <button v-if="code" class="code-toggle-btn" :class="{ active: showCode }" @click="showCode = !showCode">
                <span class="icon">{{ showCode ? '✕' : '✓' }}</span>
                {{ showCode ? '隐藏代码' : '显示代码' }}
            </button>
        </div>

        <!-- Code Block -->
        <transition name="code-fade">
            <div v-if="showCode && code" class="demo-block-code">
                <pre><code ref="codeEl" class="language-typescript">{{ code }}</code></pre>
            </div>
        </transition>
    </div>
</template>

<style scoped>
.demo-block {
    border: 1px solid #e5e7eb;
    border-radius: 8px;
    margin: 24px 0;
    overflow: hidden;
    background-color: #fff;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
}

.demo-block-header {
    padding: 16px 20px;
    border-bottom: 1px solid #f3f4f6;
}

.demo-block-title {
    margin: 0 0 8px 0;
    font-size: 16px;
    font-weight: 600;
    color: #111827;
}

.demo-block-description {
    margin: 0;
    font-size: 14px;
    color: #6b7280;
}

.demo-block-preview {
    padding: 20px;
    background-color: #f9fafb;
    min-height: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.demo-block-toolbar {
    padding: 12px 20px;
    background-color: #f3f4f6;
    display: flex;
    justify-content: flex-end;
    border-top: 1px solid #e5e7eb;
}

.code-toggle-btn {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 6px 12px;
    background-color: #fff;
    border: 1px solid #d1d5db;
    border-radius: 4px;
    font-size: 12px;
    color: #6b7280;
    cursor: pointer;
    transition: all 0.2s;
}

.code-toggle-btn:hover {
    background-color: #f3f4f6;
    border-color: #9ca3af;
    color: #374151;
}

.code-toggle-btn.active {
    background-color: #3b82f6;
    border-color: #3b82f6;
    color: #fff;
}

.icon {
    font-weight: bold;
}

.demo-block-code {
    background-color: #1f2937;
    padding: 16px 20px;
    border-top: 1px solid #e5e7eb;
    overflow-x: auto;
}

.demo-block-code pre {
    margin: 0;
    font-family: 'Courier New', Courier, monospace;
    font-size: 13px;
    line-height: 1.6;
    color: #e5e7eb;
}

/* Transition animations */
.code-fade-enter-active,
.code-fade-leave-active {
    transition: opacity 0.3s, max-height 0.3s;
}

.code-fade-enter-from,
.code-fade-leave-to {
    opacity: 0;
    max-height: 0;
}

.code-fade-enter-to,
.code-fade-leave-from {
    opacity: 1;
    max-height: 500px;
}
</style>
