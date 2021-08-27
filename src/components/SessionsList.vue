<template>
  <div
    class="grid grid-cols-1 gap-6 mt-4 md:grid-cols-2 lg:grid-cols-3 2xl:grid-cols-4 justify-items-center"
  >
    <SessionsCard v-for="(item, index) in items" :key="index" :item="item" />
  </div>
</template>

<script>
import SessionsCard from "./VariablesCard.vue"
export default {
  props: {
    items: {
      type: Array,
      required: true,
    },
  },
  components: {
    SessionsCard,
  },
}
</script>
