<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import TaskList from './components/TaskList.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

    </div>
  </header>

  <main>
    <TaskList />
  </main>
</template>