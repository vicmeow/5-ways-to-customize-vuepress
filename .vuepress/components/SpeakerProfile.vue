<template>
  <div class="speaker-profile">
    <div class="speaker-picture"><img :src="img" :alt="speaker"></div>
    <div class="speaker-info">
      <h1 class="speaker-name">{{ speaker }}</h1>
      <span>{{ twitter }}</span>
      <p class="speaker-title">{{ title }}</p>
      <div class="speaker-activities">
        <span class="speaker-activity" v-for="activity in activities" :key="activity.index">{{ activity }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['img', 'speaker', 'twitter', 'title', 'activities']
}
</script>

<style lang="sass" scoped>
.speaker-profile
  display: flex
  font-size: 1.2rem
  text-align: left
  align-items: center
  margin-top: 1rem

.speaker-picture
  flex-shrink: 0
  width: 250px
  max-height: 250px
  margin-right: 1rem
  margin-left: -1rem

  img
    border-radius: 50%
    box-shadow: -.5rem 5px 0 #3eaf7c
    object-fit: cover

p
  margin: 0

.speaker-activity
  margin-right: 1ch
</style>


