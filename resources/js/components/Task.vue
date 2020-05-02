<template>
  <tr>
    <td>
      {{ task.title }}
    </td>
    <td>
      {{ task.priority }}
    </td>
    <td>
      <button @click="remove" class="btn btn-danger">Delete</button>
    </td>
  </tr>
</template>

<script>
    export default {
      name: "Task",
      props: ['task'],
      methods: {
        remove() {
          this.$emit('delete', this.task.id);
        }
      }
    }
</script>
