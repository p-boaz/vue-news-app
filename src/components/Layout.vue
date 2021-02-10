<template>
  <Header />
  <main class="container flex-grow px-4 mx-auto mt-4">
    <slot />
  </main>
  <Footer />
</template>

<script>
import Header from "./Header.vue"
import Footer from "./Footer.vue"

export default {
  components: {
    Header,
    Footer,
  },
}
</script>
