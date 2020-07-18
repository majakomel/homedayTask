<template>
  <main>
    <div v-if="recentSearches && recentSearches.length">
      <ul>
        <li v-for="(query, index) in recentSearches" :key="index">
          <router-link :to="{ name: 'results', params: { username: query } }">{{
            query
          }}</router-link>
        </li>
      </ul>
    </div>
    <div v-else>
      No recent searches
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      recentSearches: this.$session.get("recentSearches")
    };
  }
};
</script>
