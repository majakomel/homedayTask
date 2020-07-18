<template>
  <main>
    <div>
      <div v-if="error">
        <p>There was a problem with retrieving of information: {{ error }}</p>
      </div>
      <div v-else>
        <div v-if="loading">
          <div class="la-ball la-ball-clip-rotate la-dark la-2x">
            <div></div>
          </div>
        </div>
        <div v-else>
          <section class="profileInfo">
            <div class="profileInfo__row">
              <div class="profileInfo__column">
                <img
                  :src="userInfo.avatar_url"
                  alt=""
                  class="profileInfo__img"
                />
              </div>
              <div class="profileInfo__column">
                <h1>{{ userInfo.name }}</h1>
                <div class="profileInfo__item">
                  <a :href="userInfo.html_url">{{ userInfo.login }}</a>
                </div>
                <div class="profileInfo__item">
                  <img
                    class="icon icon--location"
                    v-if="userInfo.location"
                    src="@/assets/location.svg"
                    alt=""
                  />{{ userInfo.location }}
                </div>
                <div class="profileInfo__item">{{ userInfo.company }}</div>
                <div class="profileInfo__item">
                  <a :href="userInfo.blog">{{ userInfo.blog }}</a>
                </div>
                <div class="profileInfo__item">{{ userInfo.bio }}</div>
              </div>
            </div>
          </section>

          <section v-if="userRepositories.length" class="repositories">
            <h3>Repositories:</h3>
            <ul class="repositories__list">
              <li
                v-for="repo in userRepositories"
                :key="repo.id"
                class="repositories__listItem"
              >
                <a :href="repo.html_url">{{ repo.name }}</a>
                <img
                  class="icon icon--fork"
                  v-if="repo.fork"
                  src="@/assets/code-fork.svg"
                  alt=""
                />
                <span v-if="repo.description">: {{ repo.description }}</span>
                <span v-if="repo.homepage">
                  - <a :href="repo.homepage">{{ repo.homepage }}</a></span
                >
              </li>
            </ul>
          </section>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      userInfo: null,
      userRepositories: null,
      loading: true,
      error: null
    };
  },
  mounted() {
    const username = this.$route.params.username;
    axios
      .get(`https://api.github.com/users/${username}`)
      .then(res => {
        this.userInfo = res.data;
        return axios.get(res.data.repos_url);
      })
      .then(res => {
        this.userRepositories = res.data;
        storeinSession.call(this, username);
      })
      .catch(err => {
        if (err.response && err.response.status === 404)
          this.error = `User ${username} does not exist`;
        else this.error = err;
      })
      .finally(() => {
        this.loading = false;
      });
  }
};

function storeinSession(username) {
  let recentSearches = this.$session.get("recentSearches") || [];
  recentSearches.unshift(username);
  this.$session.set("recentSearches", [...new Set(recentSearches)]);
}
</script>

<style lang="scss" scoped>
@import "../assets/styles/ball-clip-rotate.css";

.profileInfo {
  padding-bottom: 40px;

  &__row {
    display: flex;
    flex-wrap: wrap;
  }
  &__column {
    max-width: 50%;
  }
  &__item {
    margin-bottom: 10px;
  }
  &__img {
    width: calc(12.2vw + 50px);
    height: calc(12.2vw + 50px);
    border-radius: 200px;
    max-width: 220px;
    max-height: 220px;
    margin-top: 16px;
    margin-right: 3vw;
  }
}

.repositories {
  &__list {
    padding: 0;
    list-style: none;
  }
  &__listItem {
    margin-bottom: 18px;
  }
}

.icon {
  display: inline;
  width: 18px;
  &--location {
    vertical-align: text-top;
    margin-right: 6px;
  }
  &--fork {
    vertical-align: sub;
  }
}

.la-ball {
  margin: 200px auto;
}
</style>
