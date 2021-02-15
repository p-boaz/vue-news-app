<template>
  <Layout>
    <h2 class="mb-8 text-4xl font-bold text-center capitalize">
      News Section : <span class="text-green-700">{{ section }}</span>
    </h2>
    <NewsFilter v-model="section" :fetch="fetchNews" />
    <NewsList :posts="posts" />
  </Layout>
</template>

<script>
import Layout from "./components/Layout.vue"
import NewsFilter from "./components/NewsFilter.vue"
import NewsList from "./components/NewsList.vue"

const api = import.meta.env.VITE_NYT_API_KEY
import axios from "axios"

export default {
  components: {
    Layout,
    NewsFilter,
    NewsList,
  },
  data() {
    return {
      section: "home",
      posts: [],
    }
  },
  methods: {
    extractImage(post) {
      let imgObj = post.multimedia.find(
        media => media.format === "mediumThreeByTwo210"
      )
      return imgObj
    },
    async fetchNews() {
      try {
        const url = `https://api.nytimes.com/svc/topstories/v2/${this.section}.json?api-key=${api}`
        const response = await axios.get(url)
        const results = response.data.results
        this.posts = results.map(post => ({
          title: post.title,
          abstract: post.abstract,
          url: post.url,
          thumbnail: this.extractImage(post).url,
          caption: this.extractImage(post).caption,
          byline: post.byline,
          published_date: post.published_date,
        }))
      } catch (err) {
        if (err.response) {
          // client received an error response (5xx, 4xx)
          console.log("Server Error:", err)
        } else if (err.request) {
          // client never received a response, or request never left
          console.log("Network Error:", err)
        } else {
          console.log("Client Error:", err)
        }
      }
    },
  },
  mounted() {
    this.fetchNews()
  },
}
</script>
