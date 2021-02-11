<template>
  <div>
  
  
  
    <div class="d-flex">
      <div
        class="day"
        v-for="n in 30"
        :key="n"
        @drop="ondrop($event, n)"
        dropzone
        @dragover.prevent
        @dragenter.prevent
      >
        {{ n }}
        <div>
          <div v-for="(event, i) in events" :key="i">
            <div
              v-if="event.day === n"
              class="event"
              :style="[{ 'background-color': event.color }]"
              draggable
              @dragstart="startdrag($event, event)"
            >
              {{ event.name }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      events: [],
    
    }
  },
  methods: {
    ondrop(evt, n) {
      let recievedTask = JSON.parse(evt.dataTransfer.getData('task'))
      if (!recievedTask.day) {
        recievedTask.day = n

        this.events.push(recievedTask)
        this.$emit('deleteTask', recievedTask)
      } else {

        let indexOfTransferTask = this.events.findIndex(
            item => {
             return   item.name===recievedTask.name  && item.day===recievedTask.day && item.color===recievedTask.color
            }
        )
        
        this.events[indexOfTransferTask].day=n

// this.transfer = recievedTask
        // this.transferi =this.events.indexOf(this.transfer)

        // this.events[i].day=n
        // this.events.splice(i, 1)
        // recievedTask.day = n
        // this.events.push(recievedTask)
      }
    },
    startdrag(evt, event) {
      evt.dataTransfer.dropEffect = 'move'
      evt.dataTransfer.effectAllowed = 'move'
      evt.dataTransfer.setData('task', JSON.stringify(event))

      //   console.log('setted data is', evt.dataTransfer.getData('task'))
    },
  },
}
</script>
<style scoped>
.d-flex {
  display: flex;
  flex-wrap: wrap;
}
.day {
  flex-basis: 14%;
  padding: 5px;
  border: 1px solid red;
}
.event {
  color: white;
  border-radius: 3px;
}
</style>
