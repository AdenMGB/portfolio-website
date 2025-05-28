<template>
  <div class="min-h-screen bg-black text-white">
    <!-- Hero Section with Apple-style Animation -->
    <div 
      class="w-full min-h-screen flex items-center justify-center"
      v-motion
      :initial="{ opacity: 1 }"
      :enter="{ opacity: 1 }"
    >
      <div class="text-center">
        <h1 
          class="text-6xl md:text-8xl font-bold tracking-tight"
          v-motion
          :initial="{ opacity: 0, y: 20 }"
          :enter="{ opacity: 1, y: 0, transition: { duration: 600, delay: 100 } }"
        >
          Hello, I'm
        </h1>
        <h2 
          class="text-7xl md:text-9xl font-bold bg-gradient-to-r from-blue-500 to-purple-600 bg-clip-text text-transparent mt-4"
          v-motion
          :initial="{ opacity: 0, y: 20 }"
          :enter="{ opacity: 1, y: 0, transition: { duration: 600, delay: 400 } }"
        >
          AdenMGB
        </h2>
        <p 
          class="text-xl md:text-2xl mt-8 text-gray-400"
          v-motion
          :initial="{ opacity: 0 }"
          :enter="{ opacity: 1, transition: { duration: 600, delay: 700 } }"
        >
          Full Stack Developer & Designer
        </p>
      </div>
    </div>

    <!-- Main Content Section -->
    <div 
      class="min-h-screen px-4 md:px-8 pt-20"
      v-motion
      :initial="{ opacity: 0 }"
      :enter="{ 
        opacity: 1, 
        transition: { 
          duration: 1000, 
          delay: 3000 
        } 
      }"
    >
      <div class="max-w-7xl mx-auto">
        <section class="py-20">
          <h2 class="text-4xl md:text-5xl font-bold mb-8">About Me</h2>
          <p class="text-xl text-gray-300 leading-relaxed">
            Welcome to my portfolio. I'm a passionate developer focused on creating beautiful and functional digital experiences.
          </p>
        </section>

        <section class="py-20">
          <h2 class="text-4xl md:text-5xl font-bold mb-8">Projects</h2>
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            <!-- Project cards will go here -->
          </div>
        </section>

        <section class="py-20">
          <h2 class="text-4xl md:text-5xl font-bold mb-8">Contact</h2>
          <p class="text-xl text-gray-300">
            Let's connect and create something amazing together.
          </p>
        </section>

        <!-- Coding Stats Section -->
        <section class="py-20">
          <h2 class="text-4xl md:text-5xl font-bold mb-8">My Coding Stats</h2>
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            <!-- Years Coding Card -->
            <div class="rounded-2xl bg-white/10 backdrop-blur-md shadow-xl p-8 flex flex-col items-center">
              <span class="text-5xl mb-2">⌛</span>
              <div class="text-3xl font-bold">6+</div>
              <div class="text-gray-300 mt-1">Years Coding</div>
            </div>
            <!-- Followers Card -->
            <div class="rounded-2xl bg-white/10 backdrop-blur-md shadow-xl p-8 flex flex-col items-center">
              <span class="text-5xl mb-2">👥</span>
              <div class="text-3xl font-bold">2</div>
              <div class="text-gray-300 mt-1">GitHub Followers</div>
            </div>
            <!-- Pinned Projects Card -->
            <div class="rounded-2xl bg-white/10 backdrop-blur-md shadow-xl p-8 flex flex-col items-center">
              <span class="text-5xl mb-2">📌</span>
              <div class="text-3xl font-bold">2</div>
              <div class="text-gray-300 mt-1">Pinned Projects</div>
            </div>
            <!-- Main Languages Card -->
            <div class="rounded-2xl bg-white/10 backdrop-blur-md shadow-xl p-8 flex flex-col items-center col-span-1 md:col-span-2 lg:col-span-1">
              <span class="text-5xl mb-2">💻</span>
              <div class="text-2xl font-bold mb-2">Main Languages</div>
              <div class="flex gap-2 flex-wrap justify-center">
                <span class="bg-blue-600/80 text-white rounded-full px-3 py-1 text-sm font-semibold">Rust</span>
                <span class="bg-orange-500/80 text-white rounded-full px-3 py-1 text-sm font-semibold">Svelte</span>
                <span class="bg-green-600/80 text-white rounded-full px-3 py-1 text-sm font-semibold">TypeScript</span>
                <span class="bg-yellow-500/80 text-white rounded-full px-3 py-1 text-sm font-semibold">JavaScript</span>
              </div>
            </div>
            <!-- Pie Chart Card -->
            <div class="rounded-2xl bg-white/10 backdrop-blur-md shadow-xl p-8 flex flex-col items-center col-span-1 md:col-span-2 lg:col-span-1">
              <span class="text-2xl font-bold mb-2">Language Usage</span>
              <svg viewBox="0 0 36 36" class="w-24 h-24 mb-2">
                <path class="text-blue-500" d="M18 2.0845
                  a 15.9155 15.9155 0 0 1 0 31.831
                  a 15.9155 15.9155 0 0 1 0 -31.831"
                  fill="none" stroke="currentColor" stroke-width="3.5" stroke-dasharray="60, 40, 30, 70" stroke-linecap="round"/>
              </svg>
              <div class="flex gap-2 text-xs text-gray-300">
                <span class="flex items-center"><span class="w-3 h-3 bg-blue-500 rounded-full inline-block mr-1"></span>Rust</span>
                <span class="flex items-center"><span class="w-3 h-3 bg-orange-500 rounded-full inline-block mr-1"></span>Svelte</span>
                <span class="flex items-center"><span class="w-3 h-3 bg-green-600 rounded-full inline-block mr-1"></span>TypeScript</span>
              </div>
            </div>
          </div>
        </section>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
// Component logic here
</script>

<style scoped>
.bg-gradient-to-r {
  background-size: 200% 200%;
  animation: gradient 8s ease infinite;
}

@keyframes gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

/* Smooth scroll behavior for the entire page */
html {
  scroll-behavior: smooth;
}
</style> 