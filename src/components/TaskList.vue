<script setup lang="ts">
import { ref } from 'vue'
import { computed } from 'vue'
interface SubTask {
  name: string
  done: boolean
}
interface Task {
  name: string
  done: boolean
  subTasks: SubTask[]
}

const tasks = ref<Task[]>([
  { name: 'A', done: false, subTasks: [] },
  { name: 'B', done: false, subTasks: [] }
])
const finishedTasks = computed(() => tasks.value.filter((task) => task.done === true))
const notFinishedTasks = computed(() => tasks.value.filter((task) => task.done === false))
const newTaskName = ref('')
const newSubTaskName = ref('')

const addTask = () => {
  if (newTaskName.value !== '')
    tasks.value.push({ name: newTaskName.value, done: false, subTasks: [] })
  newTaskName.value = ''
}

const addSubTask = (task: Task) => {
  if (newSubTaskName.value !== '') task.subTasks.push({ name: newSubTaskName.value, done: false })
  newSubTaskName.value = ''
}
</script>

<template>
  <div>
    <ul>
      <div>未完了タスク</div>
      <li v-for="task in notFinishedTasks" :key="task.name">
        <div>タスク名: {{ task.name }}</div>
        <button @click="task.done = true">完了</button>
        <label>
          サブタスク名：
          <input v-model="newSubTaskName" type="text" />
        </label>
        <button @click="addSubTask(task)">サブタスクを追加</button>
        <ul>
          <li v-for="subTask in task.subTasks" :key="subTask.name">
            <div>サブタスク名: {{ subTask.name }}</div>
            <button @click="subTask.done = true">完了</button>
          </li>
        </ul>
      </li>
      <div>完了済タスク</div>
      <li v-for="task in finishedTasks" :key="task.name">
        <div>タスク名: {{ task.name }}</div>
        <button @click="task.done = false">未完了に戻す</button>
        <label>
          サブタスク名：
          <input v-model="newSubTaskName" type="text" />
        </label>
        <button @click="addSubTask(task)">サブタスクを追加</button>
        <ul>
          <li v-for="subTask in task.subTasks" :key="subTask.name">
            <div>サブタスク名: {{ subTask.name }}</div>
            <button @click="subTask.done = true">完了</button>
          </li>
        </ul>
      </li>
    </ul>
    <div>
      <label>
        タスク名：
        <input v-model="newTaskName" type="text" />
      </label>
    </div>
    <button @click="addTask">タスクを追加</button>
  </div>
</template>

<style></style>
