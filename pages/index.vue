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

    <!-- Animated Background and Header -->
    <transition name="fade" mode="out-in">
      <div v-if="showMainUI" key="main-ui">
        <!-- Header -->
        <header class="fixed top-0 left-0 w-full z-20 flex items-center justify-between px-8 py-4 bg-black/40 backdrop-blur-md border-b border-white/10 shadow-lg animate-fade-in">
          <div class="flex items-center gap-2">
            <span class="w-8 h-8 bg-gradient-to-br from-blue-400 to-purple-500 rounded-full flex items-center justify-center font-bold text-xl">A</span>
            <span class="font-bold text-lg tracking-wide">AdenMGB</span>
          </div>
          <nav class="flex gap-8 text-gray-200 font-medium">
            <a href="#about" class="hover:text-blue-300 transition-colors">About</a>
            <a href="#projects" class="hover:text-blue-300 transition-colors">Projects</a>
            <a href="#stats" class="hover:text-blue-300 transition-colors">Stats</a>
            <a href="#contact" class="hover:text-blue-300 transition-colors">Contact</a>
          </nav>
        </header>
      </div>
    </transition>

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


        <section class="py-20 flex flex-col gap-16">
          <!-- Hero/Intro Section -->
          <div class="relative flex flex-col items-center justify-center min-h-[40vh] text-center">
            <div class="absolute inset-0 bg-gradient-to-br from-blue-900/40 via-purple-900/30 to-black/80 blur-2xl rounded-3xl pointer-events-none animate-pulse"></div>
            <h1 class="relative z-10 text-5xl md:text-7xl font-extrabold tracking-tight bg-gradient-to-r from-blue-400 via-purple-400 to-pink-400 bg-clip-text text-transparent drop-shadow-lg mb-4 animate-fade-in">Hello, I'm Aden Lindsay</h1>
            <p class="relative z-10 text-xl md:text-2xl text-gray-200 font-medium animate-fade-in">High School Student & Passionate Developer</p>
          </div>

          <!-- About Section -->
          <div class="relative max-w-3xl mx-auto bg-white/10 backdrop-blur-2xl rounded-3xl shadow-2xl p-10 flex flex-col md:flex-row items-center gap-6 border border-white/20 hover:scale-[1.02] transition-transform duration-300 group" id="about">
            <div class="flex-shrink-0 flex flex-col items-center justify-center w-28">
              <img v-if="githubData?.avatar_url" :src="githubData.avatar_url" :alt="githubData?.name || 'Aden Lindsay'" class="w-20 h-20 rounded-full border-4 border-purple-400 shadow-lg mb-2" />
              <CodeBracketIcon v-else class="w-12 h-12 text-purple-300 group-hover:text-purple-100 transition-colors" />
              <span class="text-xs text-purple-200 mt-1">Joined {{ githubData?.created_at ? formatDate(githubData.created_at) : '' }}</span>
            </div>
            <div>
              <h2 class="text-2xl font-bold mb-2 text-purple-200">{{ githubData?.name || 'Aden Lindsay' }}</h2>
              <p class="text-gray-100 text-lg leading-relaxed mb-2">
                {{ githubData?.bio || 'I code for the love of it, always learning and building.' }}
              </p>
              <div class="flex flex-wrap gap-4 text-sm text-purple-100">
                <span v-if="githubData?.location" class="flex items-center gap-1"><svg class="w-4 h-4 text-green-400" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M15 10.5a3 3 0 11-6 0 3 3 0 016 0z"/><path stroke-linecap="round" stroke-linejoin="round" d="M19.5 10.5c0 7-7.5 11-7.5 11s-7.5-4-7.5-11a7.5 7.5 0 1115 0z"/></svg>{{ githubData.location }}</span>
                <span v-if="githubData?.html_url" class="flex items-center gap-1"><svg class="w-4 h-4 text-blue-400" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M14 3h7v7m0 0L10 21a2.828 2.828 0 01-4-4L17 3z"/></svg><a :href="githubData.html_url" target="_blank" class="underline hover:text-blue-300">GitHub</a></span>
              </div>
            </div>
          </div>

          <!-- Featured Repos & Contributions Section -->
          <div class="relative max-w-3xl mx-auto flex flex-col gap-8 my-10 animate-fade-in" id="projects">
            <div class="flex items-center gap-4 mb-2">
              <FolderIcon class="w-10 h-10 text-indigo-300" />
              <h2 class="text-2xl font-bold text-indigo-200">Featured Repos & Contributions</h2>
            </div>
            <div v-if="reposLoading" class="flex justify-center items-center min-h-[20vh]">
              <span class="text-lg text-gray-300 animate-pulse">Loading repos...</span>
            </div>
            <div v-else class="flex flex-col gap-8">
              <div v-for="repo in topRepos" :key="repo.id"
                :class="[
                  'rounded-3xl shadow-2xl p-8 border-2 transition-transform hover:scale-[1.02] group relative overflow-hidden',
                  'flex flex-col md:flex-row md:items-center gap-6',
                  languageColor(repo.language),
                  'animated-repo-card'
                ]"
              >
                <div :class="['absolute -z-10 opacity-40 blur-2xl pointer-events-none transition-all duration-700', repo.language ? 'repo-bg-' + repo.language.toLowerCase() : 'repo-bg-default']"></div>
                <div class="flex-shrink-0 flex flex-col items-center md:items-start w-20">
                  <component :is="getLangIcon(repo.language)" class="w-10 h-10 mb-2" />
                  <span v-if="repo.language" :class="['px-2 py-0.5 rounded-full font-semibold text-xs', languageBadge(repo.language)]">{{ repo.language }}</span>
                </div>
                <div class="flex-1">
                  <div class="flex items-center gap-2 mb-1">
                    <a :href="repo.html_url" target="_blank" class="text-2xl font-bold underline hover:text-blue-300 transition-colors">{{ repo.full_name || repo.name }}</a>
                    <span v-if="repo.fork" class="ml-2 text-xs bg-gray-700/60 text-gray-200 px-2 py-0.5 rounded">Fork</span>
                  </div>
                  <p class="text-gray-100 mb-2 text-lg">{{ repo.description || 'No description.' }}</p>
                  <div class="flex flex-wrap gap-4 items-center text-sm mb-2">
                    <span class="flex items-center gap-1"><svg class="w-4 h-4 text-yellow-300" fill="currentColor" viewBox="0 0 20 20"><path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.286 3.967a1 1 0 00.95.69h4.178c.969 0 1.371 1.24.588 1.81l-3.385 2.46a1 1 0 00-.364 1.118l1.287 3.966c.3.922-.755 1.688-1.54 1.118l-3.385-2.46a1 1 0 00-1.175 0l-3.385 2.46c-.784.57-1.838-.196-1.54-1.118l1.287-3.966a1 1 0 00-.364-1.118L2.045 9.394c-.783-.57-.38-1.81.588-1.81h4.178a1 1 0 00.95-.69l1.286-3.967z"/></svg>{{ repo.stargazers_count }}</span>
                    <span class="flex items-center gap-1"><svg class="w-4 h-4 text-green-300" fill="currentColor" viewBox="0 0 20 20"><path d="M5 3a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2V5a2 2 0 00-2-2H5zm10 2v.217l-5 3.125-5-3.125V5a1 1 0 011-1h8a1 1 0 011 1zm-1.197 2.618L10 10.382l-3.803-2.764L4 7.618V15a1 1 0 001 1h10a1 1 0 001-1V7.618l-1.197.736z"/></svg>{{ repo.forks_count }}</span>
                    <span class="flex items-center gap-1"><svg class="w-4 h-4 text-pink-300" fill="currentColor" viewBox="0 0 20 20"><path d="M6 2a1 1 0 00-1 1v2a1 1 0 001 1h8a1 1 0 001-1V3a1 1 0 00-1-1H6zm8 4H6v2a1 1 0 001 1h6a1 1 0 001-1V6z"/></svg>{{ formatDate(repo.updated_at) }}</span>
                  </div>
                </div>
              </div>
              <div class="flex justify-end mt-2">
                <a href="https://github.com/AdenMGB?tab=repositories" target="_blank" class="text-blue-300 underline hover:text-blue-200 transition-colors">See all on GitHub</a>
              </div>
            </div>
          </div>


          <!-- Stats Section -->
          <div class="relative max-w-3xl mx-auto bg-white/10 backdrop-blur-2xl rounded-3xl shadow-2xl p-10 border border-white/20 flex flex-col md:flex-row items-center gap-6 animate-fade-in" id="stats">
            <div class="flex-shrink-0 flex items-center justify-center w-20 h-20 rounded-full bg-gradient-to-br from-green-500/40 to-blue-500/40">
              <UsersIcon class="w-12 h-12 text-green-200" />
            </div>
            <div>
              <h2 class="text-2xl font-bold mb-2 text-green-200">Coding Stats</h2>
              <div class="flex flex-col gap-1 text-gray-100 text-lg">
                <span><span class="font-semibold">GitHub Name:</span> {{ githubData?.name || 'AdenMGB' }}</span>
                <span><span class="font-semibold">Username:</span> {{ githubData?.login || 'AdenMGB' }}</span>
                <span><span class="font-semibold">Followers:</span> {{ githubData?.followers ?? '...' }}</span>
                <span><span class="font-semibold">Following:</span> {{ githubData?.following ?? '...' }}</span>
                <span><span class="font-semibold">Public Repos:</span> {{ githubData?.public_repos ?? '...' }}</span>
                <span><span class="font-semibold">Public Gists:</span> {{ githubData?.public_gists ?? '...' }}</span>
                <span><span class="font-semibold">Location:</span> {{ githubData?.location || 'Adelaide, Australia' }}</span>
                <span><span class="font-semibold">Joined:</span> {{ githubData?.created_at ? formatDate(githubData.created_at) : '' }}</span>
              </div>
            </div>
          </div>

          <!-- Location & School Section -->
          <div class="relative max-w-4xl mx-auto grid grid-cols-1 md:grid-cols-2 gap-8 animate-fade-in">
            <div class="bg-white/10 backdrop-blur-2xl rounded-3xl shadow-2xl p-8 border border-white/20 flex items-center gap-4 hover:scale-[1.02] transition-transform">
              <svg class="w-12 h-12 text-green-400" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M15 10.5a3 3 0 11-6 0 3 3 0 016 0z"/><path stroke-linecap="round" stroke-linejoin="round" d="M19.5 10.5c0 7-7.5 11-7.5 11s-7.5-4-7.5-11a7.5 7.5 0 1115 0z"/></svg>
              <div>
                <h2 class="text-xl font-bold text-green-200 mb-1">Location</h2>
                <p class="text-gray-100 text-lg">Adelaide, Australia</p>
              </div>
            </div>
            <div class="bg-white/10 backdrop-blur-2xl rounded-3xl shadow-2xl p-8 border border-white/20 flex items-center gap-4 hover:scale-[1.02] transition-transform">
              <svg class="w-12 h-12 text-yellow-400" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M12 3v2.25M6.621 6.621l-1.591 1.591M3 12h2.25m1.371 5.379l-1.591 1.591M12 21v-2.25m5.379-1.371l1.591 1.591M21 12h-2.25m-1.371-5.379l1.591-1.591M16.5 12a4.5 4.5 0 11-9 0 4.5 4.5 0 019 0z"/></svg>
              <div>
                <h2 class="text-xl font-bold text-yellow-200 mb-1">School</h2>
                <p class="text-gray-100 text-lg">Thanks to my school for 1 year of free Cursor Pro!</p>
              </div>
            </div>
          </div>

          <!-- Philosophy/Quote Section -->
          <div class="relative max-w-2xl mx-auto bg-white/10 backdrop-blur-2xl rounded-3xl shadow-2xl p-10 border border-white/20 flex flex-col items-center animate-fade-in">
            <svg class="w-12 h-12 text-pink-400 mb-2" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M12 6v6l4 2"/></svg>
            <blockquote class="text-xl text-pink-200 font-semibold text-center italic">AI is a tool, not a replacement. Collaboration and curiosity drive progress.</blockquote>
          </div>

          <!-- Contact Section -->
          <div class="relative max-w-2xl mx-auto bg-white/10 backdrop-blur-2xl rounded-3xl shadow-2xl p-10 border border-white/20 flex flex-col items-center animate-fade-in mt-10" id="contact">
            <svg class="w-12 h-12 text-blue-400 mb-2" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M16 12H8m8 0a4 4 0 11-8 0 4 4 0 018 0zm-8 0V8a4 4 0 018 0v4"/></svg>
            <h2 class="text-2xl font-bold text-blue-200 mb-2">Contact</h2>
            <p class="text-gray-100 text-lg mb-4 text-center">Want to get in touch? Reach out via <a href="mailto:aden.lindsay@gmail.com" class="text-blue-300 underline hover:text-blue-200 transition-colors">email</a> or <a href="https://github.com/AdenMGB" target="_blank" class="text-blue-300 underline hover:text-blue-200 transition-colors">GitHub</a>.</p>
          </div>
        </section>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, computed } from 'vue'
import { Swiper, SwiperSlide } from 'swiper/vue'
import 'swiper/css'
import { UserIcon, UsersIcon, FolderIcon, CodeBracketIcon } from '@heroicons/vue/24/outline'

const githubData = ref<any>(null)
const showMainUI = ref(false)
const repos = ref<any[]>([])
const reposLoading = ref(true)

onMounted(async () => {
  const res = await fetch('https://api.github.com/users/AdenMGB')
  githubData.value = await res.json()
  setTimeout(() => {
    showMainUI.value = true
  }, 2500) // Show main UI after hero animation
  fetchRepos()
})

function formatDate(dateStr: string) {
  const date = new Date(dateStr)
  return date.toLocaleDateString(undefined, { year: 'numeric', month: 'short', day: 'numeric' })
}

async function fetchRepos() {
  // Fetch own repos
  const userReposRes = await fetch('https://api.github.com/users/AdenMGB/repos?per_page=100')
  let userRepos = await userReposRes.json()
  // Fetch starred repos (contributions)
  const starredRes = await fetch('https://api.github.com/users/AdenMGB/starred?per_page=100')
  let starredRepos = await starredRes.json()
  // Merge, dedupe by id
  const allRepos = [...userRepos, ...starredRepos]
  const uniqueRepos = Object.values(Object.fromEntries(allRepos.map(r => [r.id, r])))
  // Sort by stargazers, forks, watchers
  uniqueRepos.sort((a: any, b: any) => {
    if (b.stargazers_count !== a.stargazers_count) return b.stargazers_count - a.stargazers_count
    if (b.forks_count !== a.forks_count) return b.forks_count - a.forks_count
    return (b.watchers_count || 0) - (a.watchers_count || 0)
  })
  repos.value = uniqueRepos
  reposLoading.value = false
}

const topRepos = computed(() => repos.value.slice(0, 5))

// --- Color/Badge/Icon logic from repos.vue ---
const languageColors: Record<string, string> = {
  'TypeScript': 'border-blue-400',
  'JavaScript': 'border-yellow-400',
  'Vue': 'border-green-400',
  'Rust': 'border-orange-400',
  'Svelte': 'border-orange-300',
  'HTML': 'border-pink-400',
  'PHP': 'border-indigo-400',
  'PowerShell': 'border-blue-300',
  'default': 'border-gray-500',
}
const languageBadges: Record<string, string> = {
  'TypeScript': 'bg-blue-500/20 text-blue-200',
  'JavaScript': 'bg-yellow-500/20 text-yellow-200',
  'Vue': 'bg-green-500/20 text-green-200',
  'Rust': 'bg-orange-500/20 text-orange-200',
  'Svelte': 'bg-orange-300/20 text-orange-200',
  'HTML': 'bg-pink-500/20 text-pink-200',
  'PHP': 'bg-indigo-500/20 text-indigo-200',
  'PowerShell': 'bg-blue-300/20 text-blue-100',
  'default': 'bg-gray-700/40 text-gray-200',
}
function languageColor(lang: string) {
  return languageColors[lang] || languageColors['default']
}
function languageBadge(lang: string) {
  return languageBadges[lang] || languageBadges['default']
}
function getLangIcon(lang: string) {
  // ... same as repos.vue ...
}
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

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.8s;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
@keyframes gradient-move {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}
.animate-gradient-move {
  background-size: 200% 200%;
  animation: gradient-move 10s ease-in-out infinite;
}

.animated-repo-card {
  transition: box-shadow 0.4s, border-color 0.4s, background 0.4s;
}
.repo-bg-typescript { background: radial-gradient(circle at 80% 20%, #3b82f6 0%, transparent 70%); }
.repo-bg-javascript { background: radial-gradient(circle at 80% 20%, #facc15 0%, transparent 70%); }
.repo-bg-vue { background: radial-gradient(circle at 80% 20%, #22d3ee 0%, transparent 70%); }
.repo-bg-rust { background: radial-gradient(circle at 80% 20%, #fb923c 0%, transparent 70%); }
.repo-bg-svelte { background: radial-gradient(circle at 80% 20%, #fbbf24 0%, transparent 70%); }
.repo-bg-html { background: radial-gradient(circle at 80% 20%, #f472b6 0%, transparent 70%); }
.repo-bg-php { background: radial-gradient(circle at 80% 20%, #818cf8 0%, transparent 70%); }
.repo-bg-powershell { background: radial-gradient(circle at 80% 20%, #60a5fa 0%, transparent 70%); }
.repo-bg-default { background: radial-gradient(circle at 80% 20%, #64748b 0%, transparent 70%); }
.animated-repo-card:hover .repo-bg-typescript,
.animated-repo-card:focus .repo-bg-typescript { filter: blur(0.5rem) brightness(1.2); }
.animated-repo-card:hover .repo-bg-javascript,
.animated-repo-card:focus .repo-bg-javascript { filter: blur(0.5rem) brightness(1.2); }
.animated-repo-card:hover .repo-bg-vue,
.animated-repo-card:focus .repo-bg-vue { filter: blur(0.5rem) brightness(1.2); }
.animated-repo-card:hover .repo-bg-rust,
.animated-repo-card:focus .repo-bg-rust { filter: blur(0.5rem) brightness(1.2); }
.animated-repo-card:hover .repo-bg-svelte,
.animated-repo-card:focus .repo-bg-svelte { filter: blur(0.5rem) brightness(1.2); }
.animated-repo-card:hover .repo-bg-html,
.animated-repo-card:focus .repo-bg-html { filter: blur(0.5rem) brightness(1.2); }
.animated-repo-card:hover .repo-bg-php,
.animated-repo-card:focus .repo-bg-php { filter: blur(0.5rem) brightness(1.2); }
.animated-repo-card:hover .repo-bg-powershell,
.animated-repo-card:focus .repo-bg-powershell { filter: blur(0.5rem) brightness(1.2); }
.animated-repo-card:hover .repo-bg-default,
.animated-repo-card:focus .repo-bg-default { filter: blur(0.5rem) brightness(1.2); }
</style> 