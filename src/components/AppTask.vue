<template>
  <li
    class="todo-item"
    :class="{ 'todo-item--done': task.done }"
    @click="toggleTask"
  >
    <div class="todo-item__status">
      <i class="bi bi-check2"></i>
    </div>
    <span class="todo-item__text">{{ task.text }}</span>
    <button class="todo-item__remove-button" @click.stop="removeTask">
      <i class="bi bi-trash3"></i>
    </button>
  </li>
</template>

<script lang="ts">
import { PropType, defineComponent } from "vue";
import { Task } from "@/types/Task";

export default defineComponent({
  props: {
    task: {
      type: Object as PropType<Task>,
      required: true,
    },
  },
  methods: {
    toggleTask() {
      this.$emit("toggleTask", this.task.id);
    },
    removeTask() {
      this.$emit("removeTask", this.task.id);
    },
  },
  emits: {
    toggleTask: (id: number) => Number.isInteger(id),
    removeTask: (id: number) => Number.isInteger(id),
  },
});
</script>