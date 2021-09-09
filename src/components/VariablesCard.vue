<template>
  <section class="p-4 rounded-lg shadow-lg bg-gray-50 w-80">
    <div class="h-25">
      <h2 class="mb-2 text-lg">{{ variables.AL_DEFAULT_COUNTRY }}</h2>
        <!-- <ul class="font-mono text-sm font-light text-gray-700 transition-all duration-200 hover:text-gray-900">
            <li>{{ variables.Dingo.name }}</li>
            <li>{{ variables.Dingo.feet }}</li>
        </ul> -->
    </div>
  </section>
</template>

<script>

export default {
  props: {
    variables: {
      type: Object,
      required: true,
    },
  },
}
</script>
