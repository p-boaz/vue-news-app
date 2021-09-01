<template>
  <section class="p-4 rounded-lg shadow-lg bg-gray-50 w-80">
    <div class="h-25">
      <h2 class="mb-2 text-lg">{{ item.title }}
          <span class="inline float-right px-2 font-mono text-sm text-teal-800 align-top bg-teal-100 rounded-full animate-pulse">Tag</span></h2>
        <ul class="font-mono text-sm font-light text-gray-700 break-words transition-all duration-200 hover:text-gray-900">
            <li>{{ item.session }}</li>
            <li>{{ item.filename }}</li>
        </ul>
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
