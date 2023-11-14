<template>
  <section class="add-todo">
    <form v-if="isFormActive" class="add-todo__form">
      <button class="close-button" type="button" @click="hideForm">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input class="input" v-model="taskText" />
      </div>
      <div class="button button--filled" @click="createTask">Add task</div>
    </form>
    <button v-else class="add-todo__show-form-button" @click="showForm">
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { Task } from "../types/Task";

interface State {
  isFormActive: boolean;
  taskText: string;
}

export default defineComponent({
  data(): State {
    return {
      isFormActive: false,
      taskText: "",
    };
  },
  methods: {
    showForm() {
      this.isFormActive = true;
    },
    hideForm() {
      this.isFormActive = false;
    },
    createTask() {
      this.createEmit();
      this.cleanField();
    },
    createEmit() {
      this.$emit("createTask", {
        id: Date.now(),
        text: this.taskText,
        done: false,
      });
    },
    cleanField() {
      this.taskText = "";
    },
  },
  emits: {
    createTask: (task: Task) => task,
  },
});
</script>
