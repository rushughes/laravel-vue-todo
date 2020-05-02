<template>
  <table>
    <thead>
      <tr>
        <th>
          Task Title
        </th>
        <th>
          Priority
        </th>
        <th>
          Action
        </th>
      </tr>
    </thead>
    <tbody>
      <task-component
      v-for="task in tasks"
      :key="task.id"
      :task="task"
      @delete="remove"
      >
      </task-component>
      <tr>
        <td>
          <input
            class="form-control"
            type="text"
            id="task"
            v-model="task.title"
          />
        </td>
        <td>
          <select
            class="form-control"
            id="select"
            v-model="task.priority"
          >
              <option>
                low
              </option>
              <option>
                medium
              </option>
              <option>
                high
              </option>
          </select>
        </td>
        <td>
          <button
            class="btn btn-primary"
            @click="store"
          >
            ADD
          </button>
        </td>
      </tr>

    </tbody>
  </table>
</template>

<script>
  import TaskComponent from './Task'

  export default {
    name: "App",
    data() {
      return {
        tasks: [],
        task: {
          title: '',
          priority: ''
        }
      }
    },
    components: {
      TaskComponent
    },
    methods: {
      remove(id) {
        console.log(id)
      },
      store() {
        window.axios.post('/api/tasks/', this.task).then(({data}) => {
          console.log(data);
          this.tasks.push(data);
        })
      },
      getTasks() {
        this.tasks = [];
        window.axios.get('/api/tasks').then( ({data}) =>{
          data.forEach(task => {
            this.tasks.push(task);
            this.task.title = '';
            this.task.priority = '';
          });
        });
      }
    },
    created() {
      this.getTasks();
    }
  }
</script>
