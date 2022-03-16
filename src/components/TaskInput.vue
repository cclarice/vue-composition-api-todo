<template>
  <div class="task-input my-list">
    <input v-model="title" placeholder="Title" type="text">
    <input v-model="description" placeholder="Description" type="text">
    <button @click="onAddTask" >➕ 📃</button>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  // *
  // data () {
  //   return {
  //     title: '',
  //     description: ''
  //   }
  // },
  emits: {
    onAddTask ({ title, description }) {
      if (title === '' || description === '') {
        alert('Fill some info please!')
        return false
      }
      return true
    }
  },
  setup (props, { emit }) {
    // *
    const title = ref('')
    const description = ref('')

    const onAddTask = () => {
      emit('onAddTask', { title: title.value, description: description.value })
    }

    return {
      title,
      description,
      onAddTask
    }
  }
}
</script>

<style scoped>
.task-input {
  margin-bottom: 10px;
}
</style>
