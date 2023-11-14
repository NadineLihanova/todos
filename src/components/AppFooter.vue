<template>
  <footer class="app-footer">
    {{ statistics.active }} more to do, {{ statistics.done }} done
  </footer>
</template>

<script lang="ts">
import { PropType, defineComponent } from "vue";

export interface Statistics {
  active: number;
  done: number;
}

export default defineComponent({
  props: {
    statistics: {
      type: Object as PropType<Statistics>,
      required: true,
    },
  },
});
</script>