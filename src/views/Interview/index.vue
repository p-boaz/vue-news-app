<template>
  <Layout>
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
import SessionsFilter from "./components/SessionsFilter.vue"
import VariablesCard from "./components/VariablesCard.vue"
const api = import.meta.env.VITE_DA_API_KEY

export default {
  components: {
    Layout,
    SessionsFilter,
    VariablesCard,
  },
  data() {
    return {
      variables: {},
      session: "",
      loading: false,
      error: null,
    }
  },
  methods: {
    async fetchSession() {
    try {
      this.error = null
      this.loading = true
      const url = `https://ny.barplaybook.com/api/session?key=${api}`
      const session = `${this.session}`
      const i = `docassemble.testServer:data/questions/dict_of_objects.yml`
      const secret = `rbxUsjKfHlDuAOdr`
      axios
        .get(url,{params:{
        i: i,
        session: session,
        secret: secret,
        }})
      .then(response => (this.variables = response.data.pet.elements))
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
