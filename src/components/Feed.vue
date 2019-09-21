<template>
  <div id="feed">
    <h1>Work Feed</h1>
    <div>work</div>
  </div>
</template>

<script>
export default {
  name: 'feed',
  data: () => ({
    feedItems: {},
  }),
  created() {
    fetch('http://127.0.0.1:3000/')
      .then(response => response.json())
      .then(data => Object.assign(this.feedItems, data));
    console.log(this.feedItems);
  },
};
</script>

<style lang="scss" scoped>
#feed {
  text-align: center;
  div {
  }
}
</style>
