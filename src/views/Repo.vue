<template>
  <div class="repo">
    <div v-for="repo in repos" :key="repo.id">
      <a :href="repo.url" target="_blank">{{ repo.title }}</a>
      <p>
        {{ repo.description }}
      </p>
    </div>
  </div>
</template>
<script>
import axios from 'axios'

export default {
  data() {
    return {
      repos: []
    }
  },
  created() {
    this.fetchGithubApi()
  },
  methods: {
    async fetchGithubApi() {
      try {
        const res = await axios.get('https://api.github.com/users/schiafang/repos')
        this.repos = res.data.map(i => ({
          id: i.id,
          url: i.html_url,
          title: i.name,
          description: i.description || 'No description'
        }))
      } catch (error) {
        console.log(error)
      }
    }
  }
}
</script>