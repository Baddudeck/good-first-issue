<template>
  <div class="p-4 w-full">
    <div class="mb-6">
      <label class="block text-sm font-bold uppercase tracking-wider text-slate mb-2">
        Search repositories
      </label>
      <div class="relative">
        <MagnifyingGlassIcon
          class="absolute left-3 top-1/2 -translate-y-1/2 w-4 h-4 text-vanilla-400 pointer-events-none"
        />
        <input
          v-model="search"
          type="search"
          placeholder="Filter by name..."
          class="w-full pl-9 pr-4 py-2.5 rounded-md border border-ink-200 bg-ink-300 text-vanilla-300 placeholder-vanilla-400 focus:outline-none focus:border-juniper transition-colors"
        />
      </div>
    </div>
    <template v-if="filteredRepos.length > 0">
      <RepoBox v-for="repo in filteredRepos" :key="repo.id" :repo="repo" />
    </template>
    <p v-else class="text-vanilla-400 text-center py-8">No repositories found</p>
  </div>
</template>

<script setup>
import { MagnifyingGlassIcon } from '@heroicons/vue/24/outline'
import Repositories from '~/data/generated.json'

const search = ref('')

const filteredRepos = computed(() => {
  const q = search.value.trim().toLowerCase()
  if (!q) return Repositories
  return Repositories.filter((repo) => repo.name.toLowerCase().includes(q))
})

useHead({
  title: 'Good First Issue: Make your first open-source contribution',
  meta: [
    {
      name: 'description',
      content: 'Making your first open-source contribution is easier than you think. Good First Issue is a curated list of issues from popular open-source projects that you can easily fix. Start today!'
    }
  ]
})
</script>
