<template>
  <footer class="app-footer">{{props.stats.active}} more to do, {{props.stats.done}} done</footer>
</template>

<script setup lang="ts">
import {defineProps} from "vue";
interface Props {
  stats: {
    active: number,
    done: number
  }

}
const props = defineProps<Props>()

</script>

<style scoped>

</style>