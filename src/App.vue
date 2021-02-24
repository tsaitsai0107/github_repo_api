<template>
  <h1>{{ username }}'s repositories</h1>
  <div class="repositories">
    <div class="repository" v-for="(repo, index) in repos" :key="index">
      <div>
        <div class="title">{{ repo.name }}</div>
        <div class="text">
          {{ repo.description }}
        </div>
      </div>
      <a href="#">{{ repo.html_url }}</a>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  components: {},
  data() {
    return {
      username: "tsaitsai0107",
      repos: [],
    };
  },
  mounted() {
    const listElm = document.querySelector(".repositories");
    listElm.addEventListener("scroll", () => {
      if (listElm.scrollTop + listElm.clientHeight >= listElm.scrollHeight) {
        this.loadMore();
      }
    });

    this.loadMore();
  },
  methods: {
    loadMore() {
      axios
        .get("https://api.github.com/users/tsaitsai0107/repos")
        .then((response) => {
          this.repos = this.repos.concat(response.data);
        });
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Source+Code+Pro&family=Zilla+Slab&display=swap');
body {
  background-color: #fedfe1;
  margin: 0;
  /* box-sizing: border-box; */
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

h1 {
  text-align: center;
  font-family: 'Source Code Pro', Helvetica, Arial, sans-serif;
}

.repositories {
  margin: auto;
  width: 72vw;
  background-color: #f8c3cd;
  height: 500px;
  overflow: scroll;
  font-family: 'Zilla Slab', Helvetica, Arial, sans-serif;
}

.repository {
  display: flex;
  justify-content: space-between;
  margin: 20px 0;
  padding: 40px;
  border: 1px solid #777;
  border-radius: 8px;
}

.title {
  margin-bottom: 12px;
  font-size: 24px;
}

a {
  margin-left: 20px;
  color: #777777;
  word-wrap: break-word;
  width: 20vw;
}

@media (max-width: 991px) {
  .text {
    word-wrap: break-word;
  }
}

@media (max-width: 767px) {
  .repository {
    flex-direction: column;
  }

  a {
    margin-top: 12px;
    margin-left: 0;
    width: 100vw;
  }
}
</style>
