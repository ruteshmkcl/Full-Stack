<template>
  <div>
    <div>
      <input
        type="text"
        v-model="newTask.task"
      >
      <button @click="addTask">
        Add Task
      </button>
      <br>
      <button @click="getTask">
        Fetch all Task
      </button><br>
      <table border="2">
        <tr
          v-for="(task,id) in allTask"
          :key="id"
        >
          {{ task }}
        </tr>
      </table>
    </div>

    <div>
      Employee ID:<input
        type="number"
        v-model="emp.ID"
      ><br>
      Employee Name: <input
        type="text"
        v-model="emp.name"
      ><br>
      <!-- Employee Email: <input
        type="email"
        v-model="emp.email"
      ><br> -->
      Employee Number: <input
        type="number"
        v-model="emp.mobile"
      ><br>

      <button @click="addEmp">
        Add details
      </button>
    </div>
  </div>
</template>

<script>
import MQL from '@/plugins/mql.js'

export default {
  data () {
    return {
      newTask: {},
      allTask: [],
      emp: {}
    }
  },
  methods: {

    addEmp () {
      new MQL()
        .setActivity('o.[SaveEmployee]')
        .setData(this.emp)
        .fetch()
        .then(rs => {
          let res = rs.getActivity('SaveEmployee', true)
          if (rs.isValid('SaveEmployee')) {
            alert('Entered successfully')
            this.emp = {}
          } else {
            rs.showErrorToast('SaveEmployee')
          }
        })
    },
    addTask () {
      new MQL()
        .setActivity('o.[SaveTodoList]')
        .setData(this.newTask)
        .fetch()
        .then(rs => {
          let res = rs.getActivity('SaveTodoList', false)
          if (rs.isValid('SaveTodoList')) {
            alert('Data added successfully')
          } else {
            rs.showErrorToast('SaveTodoList')
          }
        })
    },
    getTask () {
      new MQL()
        .setActivity('o.[query_1RxKGEPZZFOrU5R3bVtUKT4ZuMl]')
        // .setData({'dynamicCollection':'cricketers'})
        .fetch()
        .then(rs => {
          let res = rs.getActivity('query_1RxKGEPZZFOrU5R3bVtUKT4ZuMl', false)
          if (rs.isValid('query_1RxKGEPZZFOrU5R3bVtUKT4ZuMl')) {
            this.allTask = res
          } else {
            rs.showErrorToast('query_1RxKGEPZZFOrU5R3bVtUKT4ZuMl')
          }
        })
    }
  }
}
</script>

<style>

</style>
