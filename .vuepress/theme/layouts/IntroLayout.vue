<template>
  <article class="frontmatter-content intro-content">
    <div class="intro">
      <h1 class="intro-heading">{{$frontmatter.heading}}</h1>
      <h2 class="intro-subheading">{{$frontmatter.subheading}}</h2>
      <p class="intro-author">by {{ $frontmatter.speaker }}</p>
    </div>
    <div class="image">
      <img :src="$frontmatter.image" class="img">
    </div>
  </article>
</template>

<style lang="sass" scoped>

.intro-content
  display: flex
  margin: 0 auto
  padding-top: 15vh

.intro-heading
  font-size: 3.3rem
  text-align: left

.intro-subheading
  font-size: 2.5rem

.intro-author
  text-align: left
  font-size: 1.2rem

.image
  align-self: center
  padding-bottom: 5rem
  min-width: 200px

</style>


