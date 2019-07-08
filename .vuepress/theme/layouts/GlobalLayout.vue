<template>
  <div id="global-layout" ref="fullscreen" class="global-layout" :class="$frontmatter.pageClass">
    <navigation v-if="!isFullscreen"/>
    <button class="btn btn-start" v-if="!isFullscreen" @click="startPresentation">Start</button>
    <button
      class="btn btn-close"
      v-if="isFullscreen"
      @click="endPresentation"
      :class="{'hide': hideClose}"
      @mouseenter="hideClose = !hideClose"
      @mouseleave="hideClose = !hideClose"
    >Close</button>

    <main class="layout" :class="layoutClass">
      <transition name="fade" mode="out-in">
        <component :is="layout" :key="$page.path"/>
      </transition>
    </main>
    <component :is="'SlideFooter'" :isFullscreen="isFullscreen"/>
  </div>
</template>

<script>
import Navigation from "../components/Navigation";
import SlideFooter from "../components/SlideFooter";
const TopicLayout = () => import("../layouts/TopicLayout");
const IntroLayout = () => import("../layouts/IntroLayout");
export default {
  components: {
    Navigation,
    SlideFooter,
    TopicLayout,
    IntroLayout
  },
  data() {
    return {
      isFullscreen: false,
      hideClose: false
    };
  },
  methods: {
    startPresentation() {
      this.isFullscreen = true;
      this.$refs["fullscreen"].requestFullscreen();
    },
    endPresentation() {
      this.isFullscreen = false;
      if (document.exitFullscreen) {
        document.exitFullscreen();
      }
    },
    toPrevious() {
      if (this.$page.path.match(/slides/g)) {
        const prev =
          this.slidePath - 1 === 0 ? "/" : "/slides/" + (this.slidePath - 1);
        this.$router.push(prev);
      }
      if (this.$frontmatter.prev) {
        this.$router.push(this.$frontmatter.prev);
      }
      if (this.slidePath === "/") {
        this.$router.push("/slides/" + this.slides);
      }
    },
    toNext() {
      const regex = /slides/g;
      if (this.$frontmatter.next) {
        this.$router.push(this.$frontmatter.next);
      }
      if (regex.test(this.$page.path)) {
        // if slide path is more than available slides, return home
        const next =
          this.slidePath === this.slides
            ? "/"
            : "/slides/" + (this.slidePath + 1);
        this.$router.push(next);
      }
    }
  },
  computed: {
    slidePath() {
      if (this.$page.path.match(/slides/g)) {
        const slidePath = this.$page.path.match(/[1-9].*/g);
        return parseInt(slidePath[slidePath.length - 1]);
      }
      return this.$page.path;
    },
    slides() {
      return this.$site.pages.filter(page => page.path.match(/slides/g)).length;
    },
    layout() {
      if (this.$page.path) {
        if (this.$frontmatter.layout) {
          return this.$frontmatter.layout + "-layout";
        }
        return "Layout";
      }
      return "NotFound";
    },
    layoutClass() {
      const layout = this.$frontmatter.layout
        ? `${this.$frontmatter.layout}-layout`
        : "";
      const fullscreen = this.isFullscreen ? "fullscreen-layout" : "";
      const fullWidth = this.$frontmatter.fullwidth ? "fullwidth-layout" : "";
      return [fullscreen, layout, fullWidth];
    },
    progress() {
      const totalSlides = this.$site.pages.length;
      const pct = totalSlides / 100;
      return pct;
    }
  },
  mounted() {
    if (this.$page.path === "/" || this.$page.path.match(/slides/g)) {
      window.addEventListener("keydown", event => {
        if (event.keyCode === 39) this.toNext();
        if (event.keyCode === 37) this.toPrevious();
        if (event.keyCode === 27) this.endPresentation();
      });
    }
  }
};
</script>
<style lang="sass"> @import '../styles/global.sass' </style>