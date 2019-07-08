<template>
  <article 
    class="frontmatter-content topic-content">
    <h1 v-if="$frontmatter.topic" class="topic-heading" :class="{'topic-long': $frontmatter.topic.split('').length > 25 }">{{ $frontmatter.topic }}</h1>
    <p v-if="$frontmatter.heading" class="sub-heading">{{ $frontmatter.heading }}</p>
    <Content />
  </article>
</template>

<style lang="sass" scoped>

.topic-content
  margin-top: 15vh

.topic-long
  max-width: 15ch

.topic-heading
  font-size: 2.3rem
  margin: 0 auto

.sub-heading
  font-size: 2em
</style>
