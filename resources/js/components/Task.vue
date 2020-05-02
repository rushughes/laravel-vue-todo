<template>
  <tr>
    <td>
      {{ task.title }}
    </td>
    <td>
      {{ task.priority }}
    </td>
    <td>
      <button class="btn btn-danger">Delete</button>
    </td>
  </tr>
</template>

<script>
    export default {
      name: "Task",
      data() {

      },
      props: ['task']
    }
</script>
