<template>
  <div class="container mt-5 main">

    <h1 class="mb-4">TODO App</h1>

    <!-- Priority -->
    <div class="row gx-5 mb-2 mt-4">

      <div class="col-md-3 col-sm-12 mb-3">
        <div class="card count" style="width: 100%">
          <div class="card-body text-center">
            <h6 class="card-subtitle mb-2 text-body-secondary">Pending</h6>
            <h5 class="card-title">{{ allTask }}</h5>
          </div>
        </div>
      </div>
      <div class="col-md-3 col-sm-12 mb-3">
        <div class="card count" style="width: 100%">
          <div class="card-body text-center">
            <h6 class="card-subtitle mb-2 text-body-secondary">Low Priority</h6>
            <h5 class="card-title">{{ taskLow }}</h5>
          </div>
        </div>
      </div>
      <div class="col-md-3 col-sm-12 mb-3">
        <div class="card count" style="width: 100%">
          <div class="card-body text-center">
            <h6 class="card-subtitle mb-2 text-body-secondary">Medium Priority</h6>
            <h5 class="card-title">{{ taskMedium }}</h5>
          </div>
        </div>
      </div>
      <div class="col-md-3 col-sm-12 mb-3">
        <div class="card count" style="width: 100%">
          <div class="card-body text-center">
            <h6 class="card-subtitle mb-2 text-body-secondary">High Priority</h6>
            <h5 class="card-title">{{ taskHigh }}</h5>
          </div>
        </div>
      </div>

    </div>


    <!-- Form -->
    <div class="card pt-2 pb-2">
       <div class="card-body align-items-center justify-content-center">
        <form class="row" @submit.prevent="addTaskList">
          <div class="col-md-4 col-sm-12">
            <label for="name">Name</label>
            <input type="text" 
              class="form-control" 
              id="name" 
              placeholder="Input task" 
              style="width:100%" 
              v-model="newTask.name"
              required>
          </div>
          <div class="col-md-4 col-sm-12">
            <label for="inputPassword2" >Priority</label>
            <select class="form-select" 
              aria-label="Input your task" 
              v-model="newTask.priority"
              required>
              <option value="Low">Low</option>
              <option value="Medium">Medium</option>
              <option value="High">High</option>
            </select>
          </div>
          <div class="col-md-4 col-sm-12">
            <button type="submit" class="btn btn-success mt-4" style="width:100%">Save</button>
          </div>
        </form>
      </div>
    </div>

    <!-- Task TODO -->
    <div class="row my-4">
      <div class="col-md-6">
        <h3>TODO</h3>
        <div class="card task pt-2 pb-2 mb-3" v-for="(task, index) in taskList" :key="index">
          <div class="card-body">
              <div class="row mb-2">
                <h6 for="name">{{ task.name }}</h6>
              </div>
              <div class="row">
                <div class="col-md-4 col-sm-4">
                  <p :class="{'high': task.priority === 'High', 
                    'low': task.priority === 'Low', 
                    'medium': task.priority === 'Medium', 
                    'p-1': true, 'text-center': true, 'priority': true}">
                    {{ task.priority }}
                  </p>
                </div>
                <div class="col-md-8 col-sm-8 space-3 text-md-end text-sm-center">
                  <button class="btn btn-danger px-3 mx-1 small" 
                    @click="removeTaskList(index)">
                    Delete
                  </button>
                  <button class="btn btn-success px-3 mx-2 small" 
                    @click="doneTask(index)">
                    Done
                  </button>
              </div>
            </div>
            </div>
       </div>
      </div>

      <!-- Task DONE -->
      <div class="col-md-6">
        <h3>DONE</h3>
          <div class="card task pt-2 pb-2 mb-3" v-for="(done, index) in taskDone" :key="index">
          <div class="card-body">
              <div class="row mb-2">
                <h6 for="name">{{ done.name }}</h6>
              </div>
              <div class="row">
                <div class="col-md-4 col-sm-4">
                  <p :class="{'high': done.priority === 'High', 
                    'low': done.priority === 'Low', 
                    'medium': done.priority === 'Medium', 
                    'p-1': true, 'text-center': true, 'priority': true}">
                    {{ done.priority }}
                  </p>
                </div>
                <div class="col-md-8 col-sm-8 space-3 text-md-end text-sm-center">
                  <button class="btn btn-danger px-3 mx-1 small"  
                    @click="removeDoneList(index)">
                    Delete
                  </button>
                  <button class="btn btn-warning px-3 mx-2 small" 
                    @click="undoneTask(index)">
                    Undone
                  </button>
              </div>
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
      newTask: { name: "", priority: "" }, // data baru
      taskList: JSON.parse(localStorage.getItem("taskList")) || [ // list data
        { name: "Makan (example)", priority: "High" }, // default
        { name: "Tidur (example)", priority: "Low" },
      ],
      taskDone: JSON.parse(localStorage.getItem("taskDone")) || [ // list data done
        { name: "Main game (example)", priority: "High" },
      ],
    };
  },
  methods:{
    addTaskList() { // add new task to list
      if (this.newTask.name && this.newTask.priority) {
        let newTask = {
          name: this.newTask.name,
          priority: this.newTask.priority,
          finish: false
        }
        this.taskList.push(newTask);
        localStorage.setItem('taskList', JSON.stringify(this.taskList));
        this.newTask = { name: "", priority: "" }; 
      } 
      alert("Add new task is successful!") //  alert if success
    },
    removeTaskList(index){ // delete task at list
      this.taskList.splice(index, 1);
      localStorage.setItem('taskList', JSON.stringify(this.taskList));
    },
    doneTask(index){ // marking task as done
      let task = this.taskList.splice(index, 1);
      this.taskDone.push(task[0]);
      localStorage.setItem('taskDone', JSON.stringify(this.taskDone)); 
      localStorage.setItem('taskList', JSON.stringify(this.taskList));
    },
    removeDoneList(index){ // remove task in done list
      this.taskDone.splice(index, 1);
      localStorage.setItem('taskDone', JSON.stringify(this.taskDone));
    },
    undoneTask(index){ // undone
      let task = this.taskDone.splice(index, 1);
      this.taskList.push(task[0]);
      localStorage.setItem('taskDone', JSON.stringify(this.taskDone)); 
      localStorage.setItem('taskList', JSON.stringify(this.taskList));
    },
  },
  computed: { // to count on things
    allTask() {
      return this.taskList.length;
    },
    taskHigh() {
      let count = this.taskList.filter(task => task.priority === 'High').length;
      return count;
    },
    taskMedium() {
      let count = this.taskList.filter(task => task.priority === 'Medium').length;
      return count;
    },
    taskLow() {
      let count = this.taskList.filter(task => task.priority === 'Low').length;
      return count;
    },
 
  }
}
</script>

<style>

  * {
    color : #2F2F2F;
  }

  .main{
    width: 70%;
  }

  .priority {
    border-radius: 30px;
    
  }

  .high {
    background-color: rgba(255, 150, 150, 0.3);
  }

  .low {
    background-color: rgba(0, 0, 255, 0.3);
  }

  .medium {
    background-color: rgba(255, 165, 0, 0.3); ;
  }

  .small {
    margin-left: 15px;
  }

  .count:hover {
    transform: scale(1.05);
    box-shadow: 0 0 10px rgba(144, 238, 144, 0.8); 
  }

  .task:hover {
    box-shadow: 0 0 5px rgba(144, 238, 144, 0.5);
  }

  .form-control:focus{
    box-shadow: none;
    border: 3px solid rgba(144, 238, 144, 0.8)
  }

   .form-select:focus{
    box-shadow: none;
    border: 3px solid rgba(144, 238, 144, 0.8)
  }

  @media (max-width: 768px) {
    .main{
    width: 100%
    }
  }

  @media screen and (min-width : 768px) and (max-width : 1024px) {
    .main{
      width: 90%
    }
  }

</style>
