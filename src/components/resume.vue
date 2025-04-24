<template>
  <div class="min-h-screen bg-gradient-to-br from-gray-900 via-blue-950 to-gray-900 text-white flex flex-col items-center justify-center px-4 sm:px-6 lg:px-8 py-12">
    <!-- Main Content -->
    <main class="flex-1 flex flex-col items-center justify-center w-full max-w-5xl">
      <h1 class="text-4xl sm:text-5xl md:text-6xl font-extrabold mb-12 tracking-tight animate-slide-in text-center">
        My Tech Stack
      </h1>

      <!-- Skills List with Progress Bars -->
      <div class="w-full grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <div
          v-for="skill in skills"
          :key="skill.name"
          class="flex flex-col p-5 bg-gray-800/70 rounded-xl hover:bg-blue-900/70 transition-all duration-300 group shadow-lg hover:shadow-blue-500/20"
        >
          <div class="flex items-center space-x-4 mb-3">
            <span class="w-8 h-8 text-2xl" :class="skill.iconClass">
              <component :is="skill.icon" />
            </span>
            <span class="text-xl font-semibold group-hover:text-blue-300 transition-colors">
              {{ skill.name }}
            </span>
          </div>
          <div class="flex items-center space-x-2">
            <div class="w-full bg-gray-700/50 rounded-full h-2.5 overflow-hidden">
              <div
                class="h-full rounded-full bg-gradient-to-r from-blue-500 to-blue-300 transition-all duration-500"
                :style="{ width: `${skill.level * 20}%` }"
              ></div>
            </div>
            <span class="text-sm text-gray-400">{{ skill.level }}/5</span>
          </div>
        </div>
      </div>

      <!-- Buttons -->
      <div class="flex flex-col sm:flex-row space-y-4 sm:space-y-0 sm:space-x-6 mt-16">
        <a
          href="#contact"
          class="bg-gradient-to-r from-blue-600 to-blue-700 hover:from-blue-700 hover:to-blue-800 text-white font-semibold py-3 px-8 rounded-full transition-all duration-300 transform hover:scale-105 hover:shadow-lg"
        >
          Hire Me!
        </a>
        <a
          href="#cv"
          class="bg-transparent border-2 border-blue-500 hover:bg-blue-600 hover:border-transparent text-white font-semibold py-3 px-8 rounded-full transition-all duration-300 transform hover:scale-105 hover:shadow-lg"
        >
          Download CV
        </a>
      </div>
    </main>
  </div>
</template>

<script>
import { defineComponent } from 'vue';
import { Icon } from '@iconify/vue';

export default defineComponent({
  name: 'Resume',
  components: { Icon },
  data() {
    return {
      skills: [
        {
          name: 'Vue.js',
          level: 4,
          icon: 'logos:vue',
          iconClass: 'text-green-400 group-hover:text-blue-300',
        },
        {
          name: 'Tailwind',
          level: 4,
          icon: 'logos:tailwindcss-icon',
          iconClass: 'text-cyan-400 group-hover:text-blue-300',
        },
        {
          name: 'Nuxt.js',
          level: 4,
          icon: 'logos:nuxt-icon',
          iconClass: 'text-green-500 group-hover:text-blue-300',
        },
        {
          name: 'Python',
          level: 4,
          icon: 'logos:python',
          iconClass: 'text-blue-400 group-hover:text-blue-300',
        },
        {
          name: 'Node.js',
          level: 3,
          icon: 'logos:nodejs-icon',
          iconClass: 'text-green-600 group-hover:text-blue-300',
        },
        {
          name: 'Laravel',
          level: 3,
          icon: 'logos:laravel',
          iconClass: 'text-red-500 group-hover:text-blue-300',
        },
        {
          name: 'TypeScript',
          level: 4,
          icon: 'logos:typescript-icon',
          iconClass: 'text-blue-600 group-hover:text-blue-300',
        },
      ],
    };
  },
});
</script>

<style scoped>
/* Custom Animations */
@keyframes slide-in {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-slide-in {
  animation: slide-in 0.8s ease-out;
}

/* Smooth Transitions */
.group:hover .transition-colors {
  transition: color 0.3s ease;
}

/* Card Hover Effects */
.group {
  transform: translateY(0);
  transition: transform 0.3s ease, background-color 0.3s ease, box-shadow 0.3s ease;
}
.group:hover {
  transform: translateY(-4px);
}

/* Ensure Icons are Properly Sized */
svg {
  width: 100%;
  height: 100%;
}
</style>