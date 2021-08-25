<template>
  <section class="p-4 rounded-lg shadow-lg bg-gray-50 w-80">
    <div class="h-96">
      <a
        class="text-xl font-bold text-center text-green-800 hover:text-green-600 hover:underline"
        target="_blank"
        rel="noreferrer"
      >
        {{ item.title }}

        {{ item.email }}
      </a>
    </div>
  </section>
</template>

<script>

export default {
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
}
</script>
