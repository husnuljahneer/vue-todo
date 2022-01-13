<template>
  <div class="container">
    <h2 class="text-center mt-5">My Vue Todo app</h2>

    <div class="d-flex">
      <input
        v-model="task"
        type="text"
        placeholder="Enter task"
        class="form-control"
      />
      <button @click="submitTask" class="btn btn-success ml-2">Submit</button>
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
        <tr v-for="(tasks, index) in tasks" :key="index">
          <td>{{ tasks.task }}</td>
          <td><span class="pointer" @click="changeStatus(index)">{{ tasks.status }}</span></td>
          <td>
            <div class="text-center" @click="editTask(index)">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="deleteTask(index)">
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
  name: "TodoComponent",
  props: {
    msg: String,
  },
  data() {
    return {
      task: "",
      editedTask: "",
      availableStatuses: ["To-do", "in-progress", "done"],
      tasks: [
        {
          task: "Learn Vue",
          status: "To-do",
        },
        {
          task: "Learn Vuex",
          status: "To-do",
        },
        {
          task: "Learn Vue Router",
          status: "To-do",
        },
      ],
    };
  },
  methods: {
    submitTask() {
      if (this.task == "") {
        alert("Please enter task");
        return;
      }

      if (this.editedTask === null) {
        this.tasks.push({
          task: this.task,
          status: "To-do",
        });
      } else {
        this.tasks[this.editedTask].task = this.task;
        this.editedTask = null;
      }
      this.task = "";
    },

    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      this.task = this.tasks[index].task;
      this.editedTask = index;
    },
    changeStatus(index) {
      this.tasks[index].status =
        this.tasks[index].status == "To-do"
          ? "in-progress"
          : this.tasks[index].status == "in-progress"
          ? "done"
          : "To-do";
    },
  },
};
</script>

<style scoped>
</style>
