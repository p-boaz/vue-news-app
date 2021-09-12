<template>
  <Layout>
    <div>
      <h2 class="mb-8 text-4xl font-bold text-center capitalize">
        Business Functions : <span class="text-green-700">{{ tag }}</span>
      </h2>
      <NewsFilter v-model="tag" :fetch="fetchItems" />
      <NewsList v-if="!loading && !error" :items="items" />
      <!-- Start of loading animation -->
      <div class="mt-40" v-if="loading">
        <p class="text-6xl font-bold text-center text-gray-500 animate-pulse">
          Loading...
        </p>
      </div>
    </div>
      <!-- End of loading animation -->

      <!-- Start of error alert -->
      <div class="mt-12 bg-red-50" v-if="error">
        <h3 class="px-4 py-1 text-4xl font-bold text-white bg-red-800">
          {{ error.title }}
        </h3>
        <p class="p-4 text-lg font-bold text-red-900">{{ error.message }}</p>
      </div>
    <!-- End of error alert -->
  </Layout>
</template>

<script>
import axios from "axios"
import Layout from "./components/Layout.vue"
import NewsFilter from "./components/NewsFilter.vue"
import NewsList from "./components/NewsList.vue"
const api = import.meta.env.VITE_DA_API_KEY

export default {
  components: {
    Layout,
    NewsFilter,
    NewsList,
  },
  data() {
    return {
      tag: "",
      items: [],
      elements: [],
      loading: false,
      error: null,
    }
  },
  methods: {
      async fetchItems() {
      try {
        this.error = null
        this.loading = true
        const url = `https://ny.barplaybook.com/api/interviews?key=${api}&tag=${this.tag}&include_dictionary=1`
        const response = await axios.get(url)
        const results = response.data.items
        this.items = results.map(item => ({
          title: item.title,
          email: item.email,
          tags: item.tags,
          filename: item.filename,
          session: item.session,
          published_date: item.published_date,
          dict: item.dict,
        }))
      } catch (err) {
        if (err.response) {
          // client received an error response (5xx, 4xx)
          this.error = {
            title: "Server Response",
            message: err.message,
          }
        } else if (err.request) {
          // client never received a response, or request never left
          this.error = {
            title: "Unable to Reach Server",
            message: err.message,
          }
        } else {
          // There's probably an error in your code
          this.error = {
            title: "Application Error",
            message: err.message,
          }
        }
      }
      this.loading = false
    },
  }
}
</script>
