<template>
  <ul class="todo-list">
    <AppTask
      v-for="task in tasks"
      :key="task.id"
      :task="task"
      @toggle-task="toggleTask(task.id)"
      @remove-task="removeTask(task.id)"
    />
  </ul>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import { Task } from "../types/Task";
import AppTask from "./AppTask.vue";

export default defineComponent({
  components: {
    AppTask,
  },
  props: {
    tasks: Array as PropType<Task[]>,
  },
  methods: {
    toggleTask(id: number) {
      this.$emit("toggleTask", id);
    },
    removeTask(id: number) {
      this.$emit("removeTask", id);
    },
  },
  emits: {
    toggleTask: (id: number) => Number.isInteger(id),
    removeTask: (id: number) => Number.isInteger(id),
  },
});
</script>