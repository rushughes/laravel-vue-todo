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
      >
      </task-component>
      <tr>
        <td>
          <input type="text" id="task" />
        </td>
        <td>
          <select id="select">
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
          <button class="btn btn-primary">ADD</button>
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
        tasks: [
          {
            id: 1,
            title: "Task 1",
            priority: "low"
          },
          {
            id: 2,
            title: "Task 2",
            priority: "medium"
          },
          {
            id: 3,
            title: "Task 3",
            priority: "high"
          }
        ]
      }
    },
    components: { TaskComponent }
  }
</script>
