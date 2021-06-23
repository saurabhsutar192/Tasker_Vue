<template>
  <div
    @dblclick="$emit('remind', task.id)"
    :class="[task.reminder ? 'tasks reminded' : 'tasks']"
  >
    <h3>{{ task.text }}</h3>
    <i @click="$emit('deleteTask', task.id)" class="fas fa-times delete"></i>
  </div>
</template>

<script>
export default {
  name: "Tasks",
  props: {
    task: Object,
  },
  emits: ["deleteTask", "remind"],
};
</script>

<style>
.tasks {
  background-color: #f2cc8f;
  width: 60vw;
  margin: 20px;
  padding: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-radius: 20px;
}

.reminded {
  background-color: #e07a5f;
}
.delete {
  cursor: pointer;
}
</style>
