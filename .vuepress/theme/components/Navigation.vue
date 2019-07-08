<template>
  <nav class="nav">
    <a class="nav-link" v-for="nav in $themeConfig.nav" :href="nav.link">{{ nav.text }}</a>
  </nav>
</template>

<style lang="sass">
.nav
  padding: 0 2rem

.nav-link
  font-size: .9rem
  text-decoration: none
  margin-right: 1rem
</style>

