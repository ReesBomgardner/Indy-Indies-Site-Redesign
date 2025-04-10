<template>
  <div class="min-h-screen bg-gray-100">
    <Gallery/>
    <AboutSection/>
  </div>
</template>

<script>
import Gallery from "./components/main.vue";
import AboutSection from "./components/about.vue";

export default {
  components: { Gallery, AboutSection }
};
</script>