<template>
  <nav id="main-nav" class="fixed top-0 left-0 w-full bg-gray-900/80 backdrop-blur-md text-white shadow-lg z-50 transition-all duration-300" :class="{ 'bg-gray-900': isScrolled }">
    <div id="nav-container" class="container mx-auto flex items-center justify-between px-6 py-4">
      <!-- Logo or Brand -->
      <div id="brand-section" class="text-3xl font-extrabold tracking-tight">
        <router-link to="/" @click="refreshPage" class="hover:text-indigo-400 hover:cursor-pointer transition-colors duration-200" style="font-family: 'Poppins', sans-serif;">
          Hedli Ahmed Khalil
        </router-link>
      </div>

      <!-- Hamburger Button for Mobile -->
      <button
        id="hamburger-menu"
        class="lg:hidden flex flex-col gap-1.5 w-8 h-8 justify-center items-center focus:outline-none"
        @click="toggleMenu"
        aria-label="Toggle navigation menu"
        aria-expanded="isMenuOpen"
      >
        <span
          class="block h-0.5 w-full bg-white rounded-full transition-transform duration-300 ease-out"
          :class="{ 'rotate-45 translate-y-2': isMenuOpen }"
        ></span>
        <span
          class="block h-0.5 w-full bg-white rounded-full transition-opacity duration-300 ease-out"
          :class="{ 'opacity-0': isMenuOpen }"
        ></span>
        <span
          class="block h-0.5 w-full bg-white rounded-full transition-transform duration-300 ease-out"
          :class="{ '-rotate-45 -translate-y-2': isMenuOpen }"
        ></span>
      </button>

      <!-- Desktop Menu -->
      <ul id="desktop-menu" class="hidden lg:flex items-center gap-8">
        <li>
          <router-link
            to="/projects"
            class="text-lg font-medium hover:text-indigo-400 hover:cursor-pointer transition-colors duration-200 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 focus:ring-offset-gray-900"
            active-class="text-indigo-400"
          >
            My Work
          </router-link>
        </li>
        <li>
          <router-link
            to="/contact"
            class="text-lg font-medium hover:text-indigo-400 hover:cursor-pointer transition-colors duration-200 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 focus:ring-offset-gray-900"
            active-class="text-indigo-400"
          >
            Contact
          </router-link>
        </li>
        <li>
          <router-link
            to="/about"
            class="text-lg font-medium hover:text-indigo-400 hover:cursor-pointer transition-colors duration-200 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 focus:ring-offset-gray-900"
            active-class="text-indigo-400"
          >
            About Me
          </router-link>
        </li>
        <li>
          <router-link
            to="/resume"
            class="text-lg font-medium hover:text-indigo-400 hover:cursor-pointer transition-colors duration-200 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 focus:ring-offset-gray-900"
            active-class="text-indigo-400"
          >
            Resume
          </router-link>
        </li>
      </ul>
    </div>

    <!-- Mobile Menu -->
    <div
      id="mobile-menu"
      v-if="isMenuOpen"
      class="lg:hidden bg-gray-900 w-full absolute top-full left-0 shadow-lg transition-all duration-300 ease-in-out"
      :class="{ 'opacity-100 translate-y-0': isMenuOpen, 'opacity-0 -translate-y-4 pointer-events-none': !isMenuOpen }"
    >
      <ul class="flex flex-col items-center py-6 space-y-4">
        <li>
          <router-link
            to="/projects"
            class="text-lg font-medium hover:text-indigo-400 hover:cursor-pointer transition-colors duration-200"
            @click="toggleMenu"
            active-class="text-indigo-400"
          >
            My Work
          </router-link>
        </li>
        <li>
          <router-link
            to="/contact"
            class="text-lg font-medium hover:text-indigo-400 hover:cursor-pointer transition-colors duration-200"
            @click="toggleMenu"
            active-class="text-indigo-400"
          >
            Contact
          </router-link>
        </li>
        <li>
          <router-link
            to="/about"
            class="text-lg font-medium hover:text-indigo-400 hover:cursor-pointer transition-colors duration-200"
            @click="toggleMenu"
            active-class="text-indigo-400"
          >
            About Me
          </router-link>
        </li>
        <li>
          <router-link
            to="/resume"
            class="text-lg font-medium hover:text-indigo-400 hover:cursor-pointer transition-colors duration-200"
            @click="toggleMenu"
            active-class="text-indigo-400"
          >
            Resume
          </router-link>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      isMenuOpen: false,
      isScrolled: false,
    };
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
    handleScroll() {
      this.isScrolled = window.scrollY > 50;
    },
    refreshPage() {
      window.location.reload();
    },
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.handleScroll);
  },
};
</script>

<style scoped>
/* Use Inter font for modern typography */
nav {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

/* Smooth transitions for links */
a {
  transition-property: color, background-color, transform;
}

/* Ensure mobile menu is hidden by default */
.pointer-events-none {
  pointer-events: none;
}
</style>