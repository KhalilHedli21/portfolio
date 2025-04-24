<template>
  <section class="relative py-12 px-4 bg-gradient-to-br from-slate-900 to-blue-950">
    <div class="max-w-5xl mx-auto">
      <h2 class="text-3xl md:text-4xl font-bold text-white mb-8">
        My Work
      </h2>

      <div class="relative overflow-hidden">
        <div
          ref="carousel"
          class="flex transition-transform duration-500 ease-in-out"
          :style="{ transform: `translateX(-${activeIndex * 100}%)` }"
          @touchstart="handleTouchStart"
          @touchmove="handleTouchMove"
          @touchend="handleTouchEnd"
        >
          <article
            v-for="(project, index) in projects"
            :key="project.id"
            class="flex-shrink-0 w-full p-2"
          >
            <div class="bg-gray-800 rounded-lg shadow-md">
              <img
                v-if="project.image"
                :src="project.image"
                :alt="project.title"
                class="w-full h-32 object-cover rounded-t-lg"
              />
              <div class="p-4">
                <h3 class="text-lg font-semibold text-white mb-1">{{ project.title }}</h3>
                <p class="text-gray-300 text-sm mb-3">{{ project.description }}</p>
                <a
                  v-if="project.github"
                  :href="project.github"
                  target="_blank"
                  rel="noopener noreferrer"
                  class="inline-block px-3 py-1 bg-blue-600 text-white text-sm rounded hover:bg-blue-700"
                  :aria-label="`View ${project.title} source code`"
                >
                  View
                </a>
              </div>
            </div>
          </article>
        </div>

        <button
          @click="prevSlide"
          class="absolute left-2 top-1/2 -translate-y-1/2 bg-white/70 hover:bg-white text-black rounded-full w-8 h-8 flex items-center justify-center"
          aria-label="Previous project"
        >
          ←
        </button>
        <button
          @click="nextSlide"
          class="absolute right-2 top-1/2 -translate-y-1/2 bg-white/70 hover:bg-white text-black rounded-full w-8 h-8 flex items-center justify-center"
          aria-label="Next project"
        >
          →
        </button>

        <div class="absolute bottom-2 left-0 right-0 flex justify-center gap-1">
          <button
            v-for="(project, index) in projects"
            :key="`dot-${project.id}`"
            @click="activeIndex = index"
            class="w-2 h-2 rounded-full"
            :class="index === activeIndex ? 'bg-white' : 'bg-white/50'"
            :aria-label="`Go to project ${index + 1}`"
          />
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue';

const projects = ref([
  {
    id: 1,
    title: 'Project One',
    description: 'A brief description of project one.',
    github: 'https://github.com/your-username/project1',
    image: 'https://via.placeholder.com/400x300'
  },
  {
    id: 2,
    title: 'Project Two',
    description: 'A brief description of project two.',
    github: 'https://github.com/your-username/project2',
    image: 'https://via.placeholder.com/400x300'
  },
  {
    id: 3,
    title: 'Project Three',
    description: 'A brief description of project three.',
    github: 'https://github.com/your-username/project3',
    image: 'https://via.placeholder.com/400x300'
  }
]);

const activeIndex = ref(0);
const touchStartX = ref(0);
const touchEndX = ref(0);

const nextSlide = () => {
  activeIndex.value = (activeIndex.value + 1) % projects.value.length;
};

const prevSlide = () => {
  activeIndex.value = (activeIndex.value - 1 + projects.value.length) % projects.value.length;
};

const handleTouchStart = (e) => {
  touchStartX.value = e.touches[0].clientX;
};

const handleTouchMove = (e) => {
  touchEndX.value = e.touches[0].clientX;
};

const handleTouchEnd = () => {
  const diff = touchStartX.value - touchEndX.value;
  if (Math.abs(diff) > 50) {
    if (diff > 0) nextSlide();
    else prevSlide();
  }
};
</script>

<style scoped>
.flex {
  display: flex;
}

.transition-transform {
  transition: transform 0.5s ease-in-out;
}

.w-full {
  width: 100%;
}

.carousel-item {
  width: 100%;
}

.carousel-item:not(:nth-child(activeIndex + 1)) {
  visibility: hidden;
}

button:focus {
  outline: 2px solid #fff;
  outline-offset: 2px;
}
</style>