<template>
  <AppHeader />

  <AppFilter :active-filter="activeFilter" @set-filter="setFilter" />

  <main class="app-main">
    <AppTaskList
      :tasks="filteredTasks"
      @toggle-task="toggleTask"
      @remove-task="removeTask"
    />

    <AppCreateTask @create-task="createTask" />
  </main>

  <AppFooter :statistics="statistics" />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AppFilter from "./components/AppFilter.vue";
import AppHeader from "./components/AppHeader.vue";
import AppTaskList from "./components/AppTaskList.vue";
import AppCreateTask from "./components/AppCreateTask.vue";
import AppFooter, { Statistics } from "./components/AppFooter.vue";
import { Task } from "./types/Task";
import { Filter } from "./types/Filter";

interface State {
  tasks: Task[];
  activeFilter: Filter;
}

export default defineComponent({
  components: {
    AppHeader,
    AppFilter,
    AppTaskList,
    AppCreateTask,
    AppFooter,
  },
  data(): State {
    return {
      tasks: [
        { id: 0, text: "Do yoga", done: false },
        { id: 1, text: "Do homework", done: false },
        { id: 2, text: "Pet the cat", done: true },
      ],
      activeFilter: "Active",
    };
  },
  computed: {
    filteredTasks(): Task[] {
      switch (this.activeFilter) {
        case "Active":
          return this.activeTasks;
        case "Done":
          return this.doneTasks;
        case "All":
        default:
          return this.tasks;
      }
    },
    statistics(): Statistics {
      return {
        active: this.activeTasks.length,
        done: this.doneTasks.length,
      };
    },
    activeTasks(): Task[] {
      return this.tasks.filter((task) => !task.done);
    },
    doneTasks(): Task[] {
      return this.tasks.filter((task) => task.done);
    },
  },
  methods: {
    createTask(task: Task) {
      this.tasks.push(task);
    },
    toggleTask(id: number) {
      const targetTask = this.tasks.find((task: Task) => task.id === id);
      if (targetTask) {
        targetTask.done = !targetTask.done;
      }
    },
    removeTask(id: number) {
      this.tasks = this.tasks.filter((task: Task) => task.id != id);
    },
    setFilter(filter: Filter) {
      this.activeFilter = filter;
    },
  },
  emits: {
    toggleTask: (id: number) => Number.isInteger(id),
    removeTask: (id: number) => Number.isInteger(id),
  },
});
</script>
