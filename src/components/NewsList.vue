<template>
  <div
    class="grid grid-cols-1 gap-6 mt-4 md:grid-cols-2 lg:grid-cols-3 2xl:grid-cols-4 justify-items-center"
  >
    <NewsCard v-for="(item, index) in items" :key="index" :item="item" />
  </div>
</template>

<script>
import NewsCard from "./NewsCard.vue"
export default {
  props: {
    items: {
      type: Array,
      required: true,
    },
  },
  components: {
    NewsCard,
  },
}
</script>
