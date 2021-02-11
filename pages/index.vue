<template>
  <div class="container">
    <div>
      <div class="tasks ">
        <div
          class="task"
          v-for="n in tasks"
          :key="n.name"
          draggable
          @dragstart="ondrag($event, n)"
          :style="[{'background-color' : n.color}]"
        >
          {{ n.name }} - {{n.color}}
        </div>
      </div>
      <mycal @deleteTask="deleteTask"></mycal>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        { name: 'task avval', date: '2021-2-8', color: 'red' },
        { name: 'task do', date: '2021-2-8', color: 'blue' },
        { name: 'task se', date: '2021-2-8', color: 'yellow' },
      ],
    }
  },
  methods: {
    ondrag(evt, n) {
      evt.dataTransfer.dropEffect = 'move'
      evt.dataTransfer.effectAllowed = 'move'
      evt.dataTransfer.setData('task', JSON.stringify(n))
      let a = evt.dataTransfer.getData('task')
    
    },
    deleteTask(task){
      
       let indexOfTransferTask = this.tasks.findIndex(
            item => {
             return   item.name===task.name  &&  item.color===task.color
            }
        )

     this.tasks.splice(indexOfTransferTask,1)
    }
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.tasks {
  display: flex;
  padding: 10px;
}
.task {
  padding: 3px;

  margin-right: 3px;
  border-radius: 3px;
  color: white;
}
</style>
