<template>
  <article class="frontmatter-content">
    <div class="frontmatter" :class="{'img-layout': $frontmatter.img }">
      <h1 v-if="$frontmatter.topic" class="topic-heading">{{ $frontmatter.topic }}</h1>
      <h2 v-if="$frontmatter.heading" class="slide-heading">{{ $frontmatter.heading }}</h2>
    </div>
    <Content/>
  </article>
</template>

<style src="prismjs/themes/prism-tomorrow.css"></style>

<style lang="sass" scoped>

.frontmatter-content
  text-align: center
  display: flex
  flex-direction: column
  margin-top: 3rem
  width: 100%

.topic-heading
  margin-top: 1rem

.img-layout
  margin-top: -2rem

</style>
