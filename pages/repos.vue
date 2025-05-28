<template>
  <div class="min-h-screen bg-black text-white px-4 md:px-8 pt-24">
    <div class="max-w-3xl mx-auto">
      <h1 class="text-5xl font-extrabold mb-10 text-center bg-gradient-to-r from-blue-400 via-purple-400 to-pink-400 bg-clip-text text-transparent drop-shadow-lg">My GitHub Repos</h1>
      <div v-if="loading" class="flex justify-center items-center min-h-[40vh]">
        <span class="text-lg text-gray-300 animate-pulse">Loading repositories...</span>
      </div>
      <div v-else class="flex flex-col gap-8">
        <div v-for="repo in sortedRepos" :key="repo.id"
          :class="[
            'rounded-3xl shadow-2xl p-8 border-2 transition-transform hover:scale-[1.02] group relative overflow-hidden',
            'flex flex-col md:flex-row md:items-center gap-6',
            languageColor(repo.language),
            'animated-repo-card'
          ]"
        >
          <!-- Animated BG blob -->
          <div :class="['absolute -z-10 opacity-40 blur-2xl pointer-events-none transition-all duration-700', repo.language ? 'repo-bg-' + repo.language.toLowerCase() : 'repo-bg-default']"></div>
          <div class="flex-shrink-0 flex flex-col items-center md:items-start w-20">
            <component :is="getLangIcon(repo.language)" class="w-10 h-10 mb-2" />
            <span v-if="repo.language" :class="['px-2 py-0.5 rounded-full font-semibold text-xs', languageBadge(repo.language)]">{{ repo.language }}</span>
          </div>
          <div class="flex-1">
            <div class="flex items-center gap-2 mb-1">
              <a :href="repo.html_url" target="_blank" class="text-2xl font-bold underline hover:text-blue-300 transition-colors">{{ repo.name }}</a>
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
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { CodeBracketIcon } from '@heroicons/vue/24/outline'

const repos = ref<any[]>([])
const loading = ref(true)

onMounted(async () => {
  const res = await fetch('https://api.github.com/users/AdenMGB/repos?per_page=100')
  let data = await res.json()
  // Sort by stargazers, then forks, then watchers
  data = data.sort((a: any, b: any) => {
    if (b.stargazers_count !== a.stargazers_count) return b.stargazers_count - a.stargazers_count
    if (b.forks_count !== a.forks_count) return b.forks_count - a.forks_count
    return (b.watchers_count || 0) - (a.watchers_count || 0)
  })
  repos.value = data
  loading.value = false
})

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
function formatDate(dateStr: string) {
  const date = new Date(dateStr)
  return date.toLocaleDateString(undefined, { year: 'numeric', month: 'short', day: 'numeric' })
}
function getLangIcon(lang: string) {
  switch (lang) {
    case 'TypeScript':
      return {
        template: '<svg class="w-7 h-7 text-blue-400" fill="currentColor" viewBox="0 0 24 24"><path d="M2 2h20v20H2V2zm11.5 15v-1.1c.6.2 1.2.3 1.8.3.7 0 1.1-.2 1.1-.6 0-.2-.1-.4-.3-.5-.2-.1-.6-.2-1.2-.4-.7-.2-1.2-.4-1.5-.7-.3-.3-.5-.7-.5-1.2 0-.6.2-1 .7-1.3.5-.3 1.1-.5 1.9-.5.6 0 1.2.1 1.7.2v1.1c-.5-.2-1-.2-1.5-.2-.7 0-1 .2-1 .5 0 .2.1.3.3.4.2.1.6.2 1.2.4.7.2 1.2.4 1.5.7.3.3.5.7.5 1.2 0 .6-.2 1-.7 1.3-.5.3-1.2.5-2 .5-.7 0-1.3-.1-1.8-.3zm-5.5-4.5h2v6h1.5v-6h2v-1.5h-5.5V12.5z"/></svg>'
      }
    case 'JavaScript':
      return {
        template: '<svg class="w-7 h-7 text-yellow-400" fill="currentColor" viewBox="0 0 24 24"><path d="M2 2h20v20H2V2zm11.5 15v-1.1c.6.2 1.2.3 1.8.3.7 0 1.1-.2 1.1-.6 0-.2-.1-.4-.3-.5-.2-.1-.6-.2-1.2-.4-.7-.2-1.2-.4-1.5-.7-.3-.3-.5-.7-.5-1.2 0-.6.2-1 .7-1.3.5-.3 1.1-.5 1.9-.5.6 0 1.2.1 1.7.2v1.1c-.5-.2-1-.2-1.5-.2-.7 0-1 .2-1 .5 0 .2.1.3.3.4.2.1.6.2 1.2.4.7.2 1.2.4 1.5.7.3.3.5.7.5 1.2 0 .6-.2 1-.7 1.3-.5.3-1.2.5-2 .5-.7 0-1.3-.1-1.8-.3zm-5.5-4.5h2v6h1.5v-6h2v-1.5h-5.5V12.5z"/></svg>'
      }
    case 'Vue':
      return {
        template: '<svg class="w-7 h-7 text-green-400" fill="currentColor" viewBox="0 0 24 24"><path d="M2 2h20v20H2V2zm10 15l-5-8.7h2.1l2.9 5.1 2.9-5.1H17L12 17z"/></svg>'
      }
    case 'Rust':
      return {
        template: '<svg class="w-7 h-7 text-orange-400" fill="currentColor" viewBox="0 0 24 24"><circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" fill="none"/><text x="12" y="16" text-anchor="middle" font-size="10" fill="currentColor">rs</text></svg>'
      }
    case 'Svelte':
      return {
        template: '<svg class="w-7 h-7 text-orange-300" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2C6.5 2 2 6.5 2 12s4.5 10 10 10 10-4.5 10-10S17.5 2 12 2zm0 18c-4.4 0-8-3.6-8-8s3.6-8 8-8 8 3.6 8 8-3.6 8-8 8zm1-13h-2v6h2V7zm0 8h-2v2h2v-2z"/></svg>'
      }
    case 'HTML':
      return {
        template: '<svg class="w-7 h-7 text-pink-400" fill="currentColor" viewBox="0 0 24 24"><path d="M2 2h20v20H2V2zm10 17l-5-8.7h2.1l2.9 5.1 2.9-5.1H17L12 19z"/></svg>'
      }
    case 'PHP':
      return {
        template: '<svg class="w-7 h-7 text-indigo-400" fill="currentColor" viewBox="0 0 24 24"><ellipse cx="12" cy="12" rx="10" ry="8" stroke="currentColor" stroke-width="2" fill="none"/><text x="12" y="16" text-anchor="middle" font-size="10" fill="currentColor">php</text></svg>'
      }
    case 'PowerShell':
      return {
        template: '<svg class="w-7 h-7 text-blue-300" fill="currentColor" viewBox="0 0 24 24"><rect x="4" y="4" width="16" height="16" rx="2" stroke="currentColor" stroke-width="2" fill="none"/><text x="12" y="16" text-anchor="middle" font-size="10" fill="currentColor">ps</text></svg>'
      }
    default:
      return CodeBracketIcon
  }
}

const sortedRepos = computed(() => repos.value)
</script>

<style scoped>
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