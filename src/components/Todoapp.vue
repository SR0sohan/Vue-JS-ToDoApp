
<template>
 <div class="container">
   <h2 class="text-center mt-5">
     Vue Todo App
   </h2>
   <div class="d-flex mt-4">
     <input v-model="task" type="text" placeholder="Enter your task" class="form-control">
     <button @click="submitTask" class="btn btn-warning rounded-0 fs-5">Submit</button>
   </div>
   <table class="table table-bordered mt-5">
     <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index">
      <td class="fs-5">
        <span :class="{'finished': task.status === 'Finished'}">
          {{ task.name}}
        </span>
        </td>
      <td style="width:150px">
        <span @click="chagesstatus(index)" class="pointer">
          {{task.status}}
          </span>
        </td>
      <td>
        <div class="text-center pointer"  @click="editTask(index)">
          <span class="fa fa-pen"></span>
        </div>
      </td>
      <td>
        <div class="text-center pointer" @click="deleteTask(index)">
          <span class="fa fa-trash "></span>
        </div>
      </td>
    </tr>
  </tbody>
   </table>
 </div>
</template>

<script >
import { ref } from 'vue'

// defineProps({
//   msg: String
// })


const count = ref(0)

export default{
  data() {
  return {
    task:'',
    editedTask:null,
    availablestatuses:['To-do','In-progress','Finished'],
    tasks: [
      {
         name:'Do something!',
         status:'To-do'
      },
    ]
   }
  },
  methods: {
    submitTask(){
      // console.log('it is clicked');
      if(this.task.length ===0) return;

      if(this.editedTask === null){
        this.tasks.push({
          name:this.task,
          status:'to-do'
        });
      }else{
        this.tasks[this.editedTask].name = this.task;
        this.editedTask= null;
      }
        this.task='';
    },
    deleteTask(index){
      this.tasks.splice(index, 1);
     },
     editTask(index){
       this.task = this.tasks[index].name;
       this.editedTask = index;
     },
    chagesstatus(index){
      let newindex =this.availablestatuses.indexOf(this.tasks[index].status);
      if(++newindex > 2) newindex= 0;
      this.tasks[index].status = this.availablestatuses[newindex];
    }

  },
  

};



</script>

<style >
.pointer{
 cursor: pointer;
}
.finished{
  text-decoration: line-through;
}
</style>
