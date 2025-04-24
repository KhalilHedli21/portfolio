<template>
  <div>
    <Navbar />
    <HeroSection />
    <AboutMe />
    <MyProjects/>
    <resume />
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import HeroSection from "@/components/HeroSection.vue";
import AboutMe from "@/components/AboutMe.vue";
import MyProjects from "./components/MyProjects.vue";
import resume from "./components/resume.vue";

export default {
  name: "App",
  components: {
    Navbar,
    HeroSection,
    AboutMe,
    MyProjects,
    resume
  },
};
</script>
