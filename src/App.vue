<script setup>
import Navbar from "./components/Navbar.vue";
import HeroSection from "./components/HeroSection.vue";
import WebProjects from "./components/WebProjects.vue";
import VideoGallery from "./components/VideoGallery.vue";
import FaqSection from './components/FaqSection.vue'
import ContactsFooter from './components/ContactsFooter.vue'
</script>

<template>
  <div class="min-h-screen flex flex-col">
    <Navbar />
    <main class="flex-1">
      <HeroSection />
      <WebProjects />
      <VideoGallery />
      <FaqSection />
    </main>
    <ContactsFooter />
  </div>
</template>
