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
      <task-component></task-component>
      <tr>
        <td>
          <input type="text" id="task" />
        </td>
        <td>
          <select id="select">
              <option>
                Low
              </option>
              <option>
                Medium
              </option>
              <option>
                High
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

    },
    components: { TaskComponent }
  }
</script>
