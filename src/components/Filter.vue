<template>
  <aside class="app-filters">
    <section class="toggle-group" >
      <button  v-for="filter in filters"
               :key="filter"
               class="button"
               :class="{'button--primary': selected === filter}"
               @click="setFilter(filter)"
      >
        {{filter}}
      </button>
    </section>
  </aside>
</template>

<script setup lang="ts">
import {defineEmits, ref} from "vue";

const filters = ref(['All', 'Active', 'Done'])
const selected =ref('All')

const setFilter =(filter)=>{
  selected.value = filter
  emit("filter", filter)
}
const emit = defineEmits<{
  (e: 'filter', filter: string): void
}>()
</script>

<style scoped>

</style>