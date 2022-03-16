<template>
  <main>
    <task-input @onAddTask="addTask"/>
    <ul class="my-list task-list">
      <li v-for="item in taskList" :key="item.id">
        <task-card :model="item"
                   @onRemove="removeTask(item.id)"
                   @onDone="setDoneTask(item.id)"/>
      </li>
    </ul>
  </main>
</template>

<script>
import TaskInput from './components/TaskInput.vue'
import TaskCard from './components/TaskCard.vue'
import { ref } from 'vue'

export default {
  name: 'App',
  components: {
    TaskCard,
    TaskInput
  },
  setup () {
    const taskList = ref([{
        id: 0,
        title: 'Create video',
        description: 'And upload on YouTube',
        status: false
      }])

    const addTask = ({ title, description }) => {
      taskList.value = [
        ...taskList.value,
        {
          id: taskList.value[0] ? taskList.value[taskList.value.length - 1].id + 1 : 0,
          title, description,
          status: false
        }
      ]
    }

    const setDoneTask = (id) => {
      taskList.value = taskList.value.map(x => {
        if (x.id === id) {
          x.status = true
        }
        return x
      })
    }

    const removeTask = (id) => {
      taskList.value = taskList.value.filter(x => x.id !== id)
    }

    return {
      taskList,
      addTask,
      setDoneTask,
      removeTask
    }
  }
}
</script>

<style scoped>
  .task-list {
    list-style: none;
  }
</style>
