<template>
  <Layout>
    <div>
      <h2 class="mb-8 text-4xl font-bold text-center capitalize">
        User List : <span class="text-green-700">{{ user_id }}</span>
      </h2>
      <NewsFilter v-model="user_id" :fetch="fetchItems" />
      <NewsList v-if="!loading && !error" :items="items" />
      <!-- Start of loading animation -->
      <div class="mt-40" v-if="loading">
        <p class="text-6xl font-bold text-center text-gray-500 animate-pulse">
          Loading...
        </p>
      </div>
    </div>
      <!-- End of loading animation -->

    <div>
      <h2 class="mb-8 text-4xl font-bold text-center capitalize">
        Session: <span class="text-green-700">{{ session }}</span>
      </h2>
      <SessionsFilter v-model="session" :fetch="fetchSession" />
      <VariablesCard :variables="variables"/>
      <!-- Start of loading animation -->
      <div class="mt-40" v-if="loading">
        <p class="text-6xl font-bold text-center text-gray-500 animate-pulse">
          Loading...
        </p>
      </div>
      <!-- End of loading animation -->

      <!-- Start of error alert -->
      <div class="mt-12 bg-red-50" v-if="error">
        <h3 class="px-4 py-1 text-4xl font-bold text-white bg-red-800">
          {{ error.title }}
        </h3>
        <p class="p-4 text-lg font-bold text-red-900">{{ error.message }}</p>
      </div>
    </div>
    <!-- End of error alert -->
  </Layout>
</template>

<script>
import axios from "axios"
import Layout from "./components/Layout.vue"
import NewsFilter from "./components/NewsFilter.vue"
import NewsList from "./components/NewsList.vue"
import SessionsFilter from "./components/SessionsFilter.vue"
import VariablesCard from "./components/VariablesCard.vue"
const api = import.meta.env.VITE_DA_API_KEY

export default {
  components: {
    Layout,
    NewsFilter,
    NewsList,
    SessionsFilter,
    VariablesCard,
  },
  data() {
    return {
      user_id: "1",
      items: [],
      variables: {},
      session: "",
      loading: false,
      error: null,
    }
  },
  methods: {
      async fetchItems() {
      try {
        this.error = null
        this.loading = true
        const url = `https://ny.barplaybook.com/api/user/${this.user_id}/interviews?key=${api}`
        const response = await axios.get(url)
        const results = response.data.items
        this.items = results.map(item => ({
          title: item.title,
          email: item.email,
          filename: item.filename,
          session: item.session,
          published_date: item.published_date,
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

    async fetchSession() {
    try {
      this.error = null
      this.loading = true
      const url = `https://ny.barplaybook.com/api/session?key=${api}`
      const session = `${this.session}`
      const i = `docassemble.SanitaryCode:data/questions/sanitary_code_standalone.yml`
      const secret = `rbxUsjKfHlDuAOdr`
      axios
        .get(url,{params:{
        i: i,
        session: session,
        secret: secret,
        }})
      .then(response => (this.variables = response.data))
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
