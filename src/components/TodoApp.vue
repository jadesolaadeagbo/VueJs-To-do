<template>
  <div class="container">
    <h2 class="text-center mt-5">My Vue Todo App</h2>
    
    <!-- Input -->
    <div class="d-flex">
      <input v-model="task" type="text" placeholder="Enter task" class="form-control">
      <button class="btn btn-warning rounded-0" @click="submitTask">SUBMIT</button>
    </div>

    <!-- Task table -->
    <table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col" class="text-center">Task</th>
      <th scope="col" class="text-center">Status</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index">
      <th>
       <span :class= "{'finished' : task.status === 'finished'}">{{task.name}}</span></th>
      <td style = "width: 120px">
        <span class="pointer" @click="changeStatus(index)">{{firstCharUpper(task.status)}}</span></td>
      <td>
        <div class="text-center" @click="editTask(index)">
          <span class="fa fa-pen"></span>
        </div>
      </td>
      <td>
        <div class = "text-center" @click="deleteTask(index)">
          <span class="fa fa-trash"></span>
        </div>
      </td>
    </tr>
    
  </tbody>
</table>

  </div>
</template>

<script>
export default {
  watch: {
  },
  name: 'HelloWorld',
  props: {
    msg: String
  },

  data(){
    return{
      task:'',
      editedTask: null,
      availableStatuses: ['to-do', 'in-progress','finished'],
      tasks: [
        {
          name:"Buy bananas from the store.",
          status:"to-do"
        },
        {
          name:"Eat 1kg chocolate in 1 hour",
          status:"in-progress"
        },
      ]
    }
  },

  methods: {
    submitTask() {
      if(this.task.length === 0) return;

      if(this.editedTask === null){
      this.tasks.push({
        name: this.task,
        status: 'to-do'
      });
    } else{
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
    }

      this.task ="";
    },
    deleteTask(index){
      this.tasks.splice(index, 1);
    },
    editTask(index){
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
    changeStatus(index){
      let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
      if(++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.availableStatuses[newIndex];
    },
    firstCharUpper(str){
      return str.charAt(0).toUpperCase() +str.slice(1);
  }
  }
}
</script>

<style scoped>
  .pointer{
    cursor: pointer;
  }
  .finished{
    text-decoration: line-through;
  }
</style>