<template>
  <div class="container">
    <div v-for="(repo, index) in repos" :key="index" class="repo-item">
      <div class="top">
        <div class="title-demo">
          <div>
            <a :href="repo.url" target="_blank" class="title"
              >{{ repo.title }} <span class="title-tip"></span
            ></a>
          </div>

          <div>
            <a
              v-if="repo.homepage"
              :href="repo.homepage"
              target="_blank"
              class="demo"
              >Demo</a
            >
          </div>
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
      repos: []
    }
  },
  created() {
    this.fetchGithubApi()
  },
  mounted() {
    const container = document.querySelector('.container')

    function throttle(fn, timeout) {
      let last, timer

      return function () {
        const context = this
        const args = arguments
        const now = + new Date()

        if (last && now < last + timeout) {
          clearTimeout(timer)
          timer = setTimeout(() => {
            last = now
            fn.apply(context, args)
          }, timeout)
        } else {
          last = now
          fn.apply(context, args)
        }
      }
    }

    const that = this
    function handleScroll() {
      if (container.scrollTop + container.clientHeight >= container.scrollHeight) {
        let temp = that.repos
        that.repos = [...temp, ...temp]
      }
    }

    container.addEventListener('scroll', throttle(handleScroll, 80))
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
  padding: 0 15px;
}

.repo-item {
  display: flex;
  flex-direction: column;
  padding: 15px 0;

  .top {
    display: flex;
    align-items: center;
    flex-direction: column;
    align-items: flex-start;
    width: 100%;
    text-align: right;
  }

  .title-demo {
    width: 100%;
    display: flex;
    flex-direction: row;
    align-items: center;
  }

  .title {
    text-decoration: none;
    font-size: 0.8rem;
    margin-right: 5px;
    padding: 3px 5px;
    color: #fff;
    background-color: #6e4555;
    position: relative;

    &:hover {
      opacity: 0.5;

      .title-tip::after {
        opacity: 1;
        top: -20px;
      }
    }
  }

  .demo {
    font-size: 0.8rem;
    text-decoration: none;
    color: #6e4555;
    font-weight: 500;

    &:hover {
      opacity: 0.5;
    }
  }

  .date {
    color: #aaa;
    font-size: 0.7rem;
    font-weight: 500;
    margin: 5px 0;
  }

  .description {
    padding: 5px 0;
    font-size: 0.8rem;
  }
}

.title-tip {
  position: absolute;

  &::after {
    content: 'Repository';
    font-size: 0.9rem;
    opacity: 0;
    position: absolute;
    top: 0;
    right: 0;
    color: #000;
    transition: all 0.2s ease-in-out;
  }
}

@media screen and (min-width: 400px) {
  .container {
    padding: 0 30px;
  }

  .repo-item {
    .top {
      display: flex;
      flex-direction: row;
      align-items: flex-end;
      justify-content: space-between;
    }

    .title-demo {
      width: auto;
    }

    .title {
      font-size: 1rem;
      padding: 5px 15px;
    }

    .demo {
      font-size: 1rem;
    }

    .date {
      margin: 0;
    }

    .description {
      font-size: 0.9rem;
    }
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