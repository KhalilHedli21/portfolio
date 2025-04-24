<template>
  <section class="relative flex items-center justify-center min-h-[calc(100vh-64px)] bg-gray-900 overflow-hidden font-inter pt-[64px]">
    <!-- Dynamic Particle Background -->
    <div class="absolute inset-0 pointer-events-none">
      <canvas ref="particleCanvas" class="w-full h-full opacity-40"></canvas>
    </div>

    <!-- Background Gradient -->
    <div class="absolute inset-0 bg-gradient-to-br from-indigo-700/30 via-gray-900/90 to-purple-700/30 transition-opacity duration-1000 ease-in-out"></div>

    <!-- Decorative Elements with Parallax -->
    <div class="absolute inset-0 pointer-events-none">
      <div class="w-40 h-40 sm:w-56 sm:h-56 bg-blue-600 opacity-20 rounded-full absolute -top-10 -left-10 sm:-top-20 sm:-left-20 blur-3xl animate-parallax" data-speed="0.25"></div>
      <div class="w-32 h-32 sm:w-48 sm:h-48 bg-purple-600 opacity-20 rounded-full absolute bottom-10 right-10 sm:bottom-20 sm:right-20 blur-3xl animate-parallax" data-speed="-0.25"></div>
    </div>

    <!-- Content -->
    <div class="relative z-10 flex flex-col lg:flex-row items-center justify-center w-full min-h-[calc(100vh-64px)] px-4 sm:px-6 lg:px-8">
      <!-- Image with Neon Frame (Full Size) -->
      <div class="relative w-full lg:w-1/2 flex justify-center items-center min-h-[40vh] sm:min-h-[50vh] lg:min-h-[calc(100vh-64px)] animate-fade-in">
        <div class="relative w-full h-full max-w-[100%] sm:max-w-[90vw] lg:max-w-[100%] min-h-[40vh] sm:min-h-[60vh] lg:min-h-[calc(100vh-64px)] rounded-3xl overflow-hidden glow transition-transform duration-500 ease-out group">
          <img
            src="@/assets/khalil-photo.png"
            alt="Khalil's Portrait"
            class="w-full h-full object-cover rounded-3xl shadow-xl transition-transform duration-300 ease-out group-hover:scale-105"
          />
          <!-- Neon Frame -->
          <div class="absolute inset-0 border-4 border-blue-500 rounded-3xl opacity-75 group-hover:opacity-100 transition-opacity duration-300" style="clip-path: polygon(0 0, 55% 0, 55% 55%, 100% 55%, 100% 100%, 0 100%);"></div>
        </div>
      </div>

      <!-- Text -->
      <div class="w-full lg:w-1/2 flex justify-center items-center min-h-[40vh] sm:min-h-[50vh] lg:min-h-[calc(100vh-64px)] py-10 lg:py-0 animate-slide-in">
        <div class="text-center lg:text-left max-w-md sm:max-w-lg lg:max-w-xl px-4 sm:px-6">
          <h1 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-extrabold text-white tracking-tight mb-4 sm:mb-6 leading-tight">
            Crafting the Future<br class="hidden sm:block" />
            <span class="text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-purple-400 typing-animation">Professional Portfolio</span>
          </h1>
          <p class="text-gray-200 text-sm sm:text-base lg:text-lg mb-6 sm:mb-8 max-w-sm sm:max-w-md mx-auto lg:mx-0">
            Dive into my world of innovation, creativity, and technical excellence.
          </p>
          <a
            href="https://linktr.ee/khalil.hedli21"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-block px-6 sm:px-8 py-2.5 sm:py-3.5 bg-gradient-to-r from-blue-600 to-purple-600 text-white text-sm sm:text-base font-medium rounded-full shadow-lg transition-all duration-300 ease-out hover:from-blue-700 hover:to-purple-700 hover:shadow-xl focus:outline-none focus:ring-4 focus:ring-blue-500/50 glow"
            aria-label="Explore Khalil's Linktree"
          >
            Explore Now
          </a>
        </div>
      </div>
    </div>

    <!-- Logo -->
    <div class="absolute bottom-4 sm:bottom-6 right-4 sm:right-6 z-20">
      <img
        src="../assets/white-logo-khalil.png"
        alt="Khalil's Logo"
        class="w-12 h-12 sm:w-14 sm:h-14 opacity-75 transition-all duration-300 hover:opacity-100 hover:scale-110"
      />
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// Particle Animation
const particleCanvas = ref(null)

onMounted(() => {
  const canvas = particleCanvas.value
  const ctx = canvas.getContext('2d')
  let particles = []
  let animationFrameId

  const isLowEndDevice = window.innerWidth < 768 || navigator.hardwareConcurrency < 4
  const particleCount = isLowEndDevice ? 30 : 60

  const resizeCanvas = () => {
    canvas.width = window.innerWidth
    canvas.height = window.innerHeight
  }

  const createParticle = () => {
    return {
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      size: Math.random() * 1.5 + 0.5,
      speedX: Math.random() * 0.4 - 0.2,
      speedY: Math.random() * 0.4 - 0.2,
      opacity: Math.random() * 0.4 + 0.2
    }
  }

  const initParticles = () => {
    particles = []
    for (let i = 0; i < particleCount; i++) {
      particles.push(createParticle())
    }
  }

  const animateParticles = () => {
    ctx.clearRect(0, 0, canvas.width, canvas.height)
    particles.forEach(particle => {
      particle.x += particle.speedX
      particle.y += particle.speedY
      if (particle.x < 0 || particle.x > canvas.width) particle.speedX *= -1
      if (particle.y < 0 || particle.y > canvas.height) particle.speedY *= -1

      ctx.beginPath()
      ctx.arc(particle.x, particle.y, particle.size, 0, Math.PI * 2)
      ctx.fillStyle = `rgba(147, 197, 253, ${particle.opacity})`
      ctx.fill()
    })
    animationFrameId = requestAnimationFrame(animateParticles)
  }

  resizeCanvas()
  initParticles()
  animateParticles()

  window.addEventListener('resize', resizeCanvas)

  // Parallax Effect
  const parallaxElements = document.querySelectorAll('.animate-parallax')
  const handleMouseMove = (e) => {
    if (isLowEndDevice) return // Skip parallax on low-end devices
    parallaxElements.forEach(el => {
      const speed = el.getAttribute('data-speed')
      const x = (window.innerWidth - e.pageX * speed) / 120
      const y = (window.innerHeight - e.pageY * speed) / 120
      el.style.transform = `translate(${x}px, ${y}px)`
    })
  }

  window.addEventListener('mousemove', handleMouseMove)

  onUnmounted(() => {
    cancelAnimationFrame(animationFrameId)
    window.removeEventListener('resize', resizeCanvas)
    window.removeEventListener('mousemove', handleMouseMove)
  })
})
</script>

<style scoped>
.font-inter {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.bg-gradient-to-br {
  background-image: linear-gradient(to bottom right, var(--tw-gradient-from), var(--tw-gradient-to));
}

.glow {
  box-shadow: 0 0 15px rgba(59, 130, 246, 0.5), 0 0 30px rgba(59, 130, 246, 0.25);
}

.animate-slide-in {
  animation: slideIn 1s ease-out forwards;
}

.animate-fade-in {
  animation: fadeIn 1.5s ease-in forwards;
}

.typing-animation {
  display: inline-block;
  overflow: hidden;
  white-space: nowrap;
  animation: typing 3s steps(30, end) forwards;
}

@keyframes slideIn {
  from {
    transform: translateY(40px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: scale(0.98);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

@keyframes typing {
  from {
    width: 0;
  }
  to {
    width: 100%;
  }
}
</style>