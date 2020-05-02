<template>
  <div class="app-component">
    <loading :active.sync="isLoading"
        :can-cancel="true"
        :on-cancel="onCancel"
        :is-full-page="fullPage"></loading>
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
  </div>
</template>

<script>
  import TaskComponent from './Task'
  // Import component
    import Loading from 'vue-loading-overlay'
    // Import stylesheet
    import 'vue-loading-overlay/dist/vue-loading.css'

  export default {
    name: "App",
    data() {
      return {
        tasks: [],
        task: {
          title: '',
          priority: ''
        },
        isLoading: false,
        fullPage: true
      }
    },
    components: {
      TaskComponent,
      Loading
    },
    methods: {
      remove(id) {
        this.isLoading = true;
        window.axios.delete(`/api/tasks/${id}`).then(()=>{
          let index = this.tasks.findIndex(task => task.id === id);
          this.tasks.splice(index,1);
          //this.getTasks();
          this.isLoading = false;
        });
      },
      store() {
        if (this.checkInputs()) {
          this.isLoading = true;
          window.axios.post('/api/tasks/', this.task).then(({data}) => {
            console.log(data);
            this.tasks.push(data);
            this.isLoading = false;
          })
        }
      },
      checkInputs() {
        if (this.task.title && this.task.priority) {
          return true;
        } else {
          return false;
        }
      },
      getTasks() {
        this.isLoading = true;
        this.tasks = [];
        window.axios.get('/api/tasks').then( ({data}) =>{
          data.forEach(task => {
            this.tasks.push(task);
            this.task.title = '';
            this.task.priority = '';
            this.isLoading = false;
          });
        });
      }
    },
    created() {
      this.getTasks();
    }
  }
</script>
