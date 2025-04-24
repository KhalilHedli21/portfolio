<template>
  <section class="about-section" id="aboutme">
    <div class="content">
      <!-- Image Container -->
      <div class="image-container">
        <div class="image-wrapper">
          <img src="../assets/image.png" alt="Hedli Ahmed Khalil" class="profile-image" />
          <div class="image-overlay"></div>
        </div>
      </div>

      <!-- Text Container -->
      <div class="text-container">
        <h1 class="animate-title">About Me</h1>
        <p class="animate-text">
          I'm <span class="highlight">Hedli Ahmed Khalil</span>, a passionate full stack Web Developer and Software Engineering student at The University of Skikda.
        </p>
        <p class="animate-text delay-1">
          I specialize in crafting <span class="highlight">functional and visually stunning</span> web experiences that leave a lasting impression.
        </p>
        <p class="animate-text delay-2">
          Always eager to <span class="highlight">learn cutting-edge technologies</span> and tackle challenging projects, I strive to deliver <span class="highlight">exceptional quality</span>.
        </p>
        <p class="animate-text delay-3">
          Let's collaborate and <span class="highlight">create something extraordinary</span> together!
        </p>
        <button class="connect-button" @click="connect">Let's Connect!</button>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'AboutMe',
  methods: {
    connect() {
      // Placeholder for connect functionality (e.g., open contact form or email)
      alert('Ready to collaborate? Reach out to me!');
    },
  },
};
</script>

<style scoped>
.about-section {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  padding: 2rem 1rem;
  background: linear-gradient(135deg, #0f1020 0%, #1a1b2d 100%);
  color: white;
  overflow: hidden;
}

.content {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 2rem;
  max-width: 1200px;
  width: 100%;
  margin: 0 auto;
}

/* Image Styling */
.image-container {
  flex: 1;
  display: flex;
  justify-content: center;
  position: relative;
}

.image-wrapper {
  position: relative;
  width: 100%;
  max-width: 320px;
  aspect-ratio: 1;
}

.profile-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 20px;
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.4);
  transition: transform 0.5s ease, filter 0.5s ease;
  z-index: 2;
}

.image-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(45deg, rgba(59, 130, 246, 0.2), rgba(16, 185, 129, 0.2));
  border-radius: 20px;
  opacity: 0;
  transition: opacity 0.5s ease;
  z-index: 1;
}

.image-wrapper:hover .profile-image {
  transform: scale(1.05) rotate(2deg);
  filter: brightness(1.1);
}

.image-wrapper:hover .image-overlay {
  opacity: 1;
}

/* Text Styling */
.text-container {
  flex: 2;
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  padding: 2rem;
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
  transition: transform 0.5s ease;
}

.text-container:hover {
  transform: translateY(-10px);
}

h1 {
  font-size: clamp(2rem, 5vw, 3rem);
  font-weight: 700;
  margin-bottom: 1.5rem;
  color: #ffffff;
  background: linear-gradient(to right, #3b82f6, #10b981);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

p {
  font-size: clamp(1rem, 2.5vw, 1.2rem);
  line-height: 1.8;
  margin-bottom: 1rem;
  color: #e5e7eb;
}

.highlight {
  background: linear-gradient(to right, #3b82f6, #10b981);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-weight: 600;
}

/* Button Styling */
.connect-button {
  margin-top: 1.5rem;
  padding: 0.75rem 2rem;
  background: linear-gradient(45deg, #3b82f6, #10b981);
  color: white;
  font-weight: 600;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.connect-button:hover {
  transform: scale(1.1);
  box-shadow: 0 5px 15px rgba(59, 130, 246, 0.4);
}

/* Animations */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-title {
  animation: fadeInUp 0.6s ease-out;
}

.animate-text {
  animation: fadeInUp 0.6s ease-out;
}

.delay-1 { animation-delay: 0.2s; }
.delay-2 { animation-delay: 0.4s; }
.delay-3 { animation-delay: 0.6s; }

/* Responsive Design */
@media (max-width: 1024px) {
  .content {
    flex-direction: column;
    gap: 3rem;
  }

  .image-container,
  .text-container {
    flex: none;
    width: 100%;
  }

  .image-wrapper {
    max-width: 280px;
  }

  .text-container {
    text-align: center;
  }
}

@media (max-width: 640px) {
  .about-section {
    padding: 2rem 1rem;
  }

  .image-wrapper {
    max-width: 220px;
  }

  h1 {
    font-size: 2rem;
  }

  p {
    font-size: 1rem;
  }

  .connect-button {
    padding: 0.6rem 1.5rem;
  }
}
</style>