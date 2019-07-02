<template lang="pug">
#app

  #input.ui.input.action
    input(type="text", v-model='todo', placeholder="add todo..." @keydown.enter='addTask()')
    button.ui.icon.button(@click='addTask()')
      i.plus.icon

  .task(v-for="task in tasks")
    .ui.checkbox(@click='toggleTask(task.name)')
      input(type="checkbox" v-model='task.toggle')
      label(v-if='!task.toggle') {{task.name}}
      label(v-if='task.toggle')
        del {{task.name}}
    i.delete.icon(v-if='task.toggle' @click='rmTask(task.name)')

</template>

<script>
export default {

  data() {return {
    todo: 'Data binding is cool!',
    tasks: []
  }},

  methods: {

    addTask(){ 
      if (!this.todo)
        return
      this.tasks.push({
        name: this.todo,
        toggle: false
      })
      this.todo = ''
    },

    rmTask(tsk) {
      this.tasks = this.tasks.filter(task => task.name != tsk)
    },

    toggleTask(tsk) {
      const toggle = this.tasks.find(task => task.name === tsk).toggle
      this.tasks.find(task => task.name === tsk).toggle = !toggle

    }
  }
}
</script>

<style lang="sass">
html
  font-size: large
#app
  width: 22em
  margin: auto
  display: flex
  flex-direction: column
  padding: 2em
.task
  margin-top: 1em
  display: flex
  justify-content: space-between
</style>
