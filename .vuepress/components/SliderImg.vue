<template>
  <figure class="slider-img">
    <img class="img" :src="src" :alt="alt">
    <figcaption class="caption">{{ caption }}</figcaption>
  </figure>
</template>

<script>
export default {
  props: ["src", "alt", "caption"]
};
</script>

<style lang="sass" scoped>
.slider-img
  display: flex
  flex-direction: column
  margin: 0
  height: 100%
  margin: .5rem
  border-radius: 10px
  overflow: hidden

.img
  min-height: 0
  object-fit: scale-down
  object-position: top

.caption
  font-size: .85rem
  font-style: italic
  background: white
  padding: .5rem 1rem
</style>

