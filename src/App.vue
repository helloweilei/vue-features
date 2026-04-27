<script setup lang="ts">
import DemoBlock from './components/DemoBlock.vue'
import DirectivesDemo from './components/DirectivesDemo.vue'


</script>

<template>
  <div class="app-container">
    <header class="app-header">
      <h1>Vue 3 功能演示</h1>
    </header>
    <main class="app-main">
      <DemoBlock title="自定义指令">
        <DirectivesDemo />
      </DemoBlock>
    </main>
  </div>
</template>

<style scoped>
.app-container {
  min-height: 100vh;
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
}

.app-header {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 40px 20px;
  text-align: center;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.app-header h1 {
  margin: 0 0 8px 0;
  font-size: 32px;
  font-weight: 700;
}

.subtitle {
  margin: 0;
  font-size: 16px;
  opacity: 0.9;
}

.app-main {
  max-width: 900px;
  margin: 40px auto;
  padding: 0 20px 40px;
}

@media (max-width: 768px) {
  .app-header h1 {
    font-size: 24px;
  }

  .app-main {
    padding: 0 16px 24px;
  }
}
</style>
