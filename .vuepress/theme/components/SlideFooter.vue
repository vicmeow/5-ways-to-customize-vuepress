<template>
  <footer class="footer slide-footer">
    <a
      class="control-link"
      v-if="!isFullscreen"
      :class="{ hidden: isFullscreen }"
      :href="$frontmatter.prev"
    >Previous</a>
    <div v-if="$page.path !== '/'">
      <span class="hashtag">@vicbergquist</span>
      <span class="hashtag" v-for="hashtag in hashtags">#{{ hashtag }}</span>
    </div>
    <div v-if="$frontmatter.event">
      <span class="hashtag">{{ $frontmatter.event }}</span>
    </div>
    <a
      class="control-link"
      v-if="!isFullscreen"
      :class="{ hidden: isFullscreen }"
      :href="$frontmatter.next"
    >Next</a>
    <!-- <progress-bar :progress="progress"/> -->
  </footer>
</template>

<script>
export default {
  props: ["isFullscreen", "progress"],
  computed: {
    hashtags() {
      return this.$frontmatter.hashtags
        ? this.$frontmatter.hashtags
        : this.$themeConfig.globalHashtags;
    }
  }
};
</script>

<style lang="sass" scoped>
.footer
  display: flex
  // flex-wrap: wrap
  justify-content: space-around
  text-align: center

.control-link
  text-decoration: none
</style>

