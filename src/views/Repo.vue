<template>
  <div class="container">
    <div v-for="(repo, index) in repos" :key="index" class="repo-item">
      <div class="top">
        <div>
          <a :href="repo.url" target="_blank" class="repo-title"
            >{{ repo.title }} <span class="repo-title-tip"></span
          ></a>
          <a
            v-if="repo.homepage"
            :href="repo.homepage"
            target="_blank"
            class="repo-demo"
            >Demo</a
          >
        </div>
        <span class="date">
          {{ repo.date }}
        </span>
      </div>
      <span class="description">
        {{ repo.description }}
      </span>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
import moment from 'moment'

export default {
  data() {
    return {
      repos: [],
      intersectionObserver: null,
      firstItem: '',
      lastItem: '',
    }
  },
  created() {
    this.fetchGithubApi()
  },
  mounted() {
    const container = document.querySelector('.container')
    container.addEventListener('scroll', () => {
      if (container.scrollTop + container.clientHeight >= container.scrollHeight) {
        let temp = this.repos
        this.repos = [...temp, ...temp]
      }
    })
  },
  methods: {
    async fetchGithubApi() {
      try {
        const res = await axios.get('https://api.github.com/users/schiafang/repos')
        this.repos = res.data.map(i => ({
          id: i.id,
          url: i.html_url,
          title: i.name,
          homepage: i.homepage,
          description: i.description || 'No description',
          timestamp: moment(`${i.created_at}`).valueOf(),
          date: i.created_at.split('').slice(0, 10).join('')
        }))

        this.repos = this.repos.sort((a, b) => b.timestamp - a.timestamp)
      } catch (error) {
        console.log(error)
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  background-color: #eee;
  border-radius: 4px;
  margin: 0 15px;
  height: calc(100vh - 100px);
  overflow-y: scroll;
  padding: 0 30px;
}

.repo-item {
  height: 50px;
  display: flex;
  flex-direction: column;
  padding: 30px 0;

  .top {
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
  }

  .date {
    color: #aaa;
    font-size: 0.8rem;
    font-weight: 500;
  }

  .description {
    padding: 15px 0;
  }
}

.repo-title {
  text-decoration: none;
  font-size: 1rem;
  margin-right: 15px;
  padding: 5px 15px;
  color: #fff;
  background-color: #6e4555;
  position: relative;

  &:hover {
    opacity: 0.5;

    .repo-title-tip::after {
      opacity: 1;
      top: -20px;
    }
  }
}

.repo-title-tip::after {
  content: 'Repository';
  font-size: 0.9rem;
  opacity: 0;
  position: absolute;
  top: 0;
  right: 0;
  color: #000;
  transition: all 0.2s ease-in-out;
}

.repo-demo {
  text-decoration: none;
  color: #6e4555;
  font-weight: 500;

  &:hover {
    opacity: 0.5;
  }
}

@media screen and (min-width: 600px) {
  .container {
    margin: 0 100px;
    height: calc(100vh - 120px);
  }

  .repo-title {
    font-size: 1.2rem;
  }
}
</style>