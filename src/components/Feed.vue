<template>
  <div class="feed">
    <h1>Work Feed</h1>
    <div v-if="loading">Loading...</div>
    <div v-else>
      <FeedItem v-for="feedItem in feedItems" :key="feedItem.Index" v-bind:feedItemData="feedItem" />
    </div>
  </div>
</template>

<script>
import FeedItem from './FeedItem.vue';

export default {
  name: 'feed',
  data: () => ({
    loading: false,
    feedItems: {},
  }),
  components: {
    FeedItem,
  },
  created() {
    this.GetData();
  },
  methods: {
    GetData() {
      this.loading = true;
      fetch('http://127.0.0.1:3000/')
        .then(response => response.json())
        .then(data => {
          Object.assign(this.feedItems, data);
          this.loading = false;
        });
    },
  },
};
</script>

<style lang="scss" scoped>
.feed {
  text-align: center;
}
</style>
