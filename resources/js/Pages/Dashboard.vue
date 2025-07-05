<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
import { ref } from 'vue';

const sidebarOpen = ref(false);

const links = [
  { name: 'Accueil', href: '/dashboard', icon: 'home' },
  { name: 'Profil', href: '/profile', icon: 'user' },
  { name: 'Paramètres', href: '/settings', icon: 'cog' },
  { name: 'Déconnexion', href: '/logout', icon: 'logout' },
];

// Fonction simple pour icônes SVG (tu peux remplacer ou étendre)
const icons = {
  home: `
    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" stroke="currentColor" stroke-width="2"
      stroke-linecap="round" stroke-linejoin="round" viewBox="0 0 24 24">
      <path d="M3 9.75L12 3l9 6.75v11.25a1.5 1.5 0 01-1.5 1.5h-15a1.5 1.5 0 01-1.5-1.5V9.75z"></path>
      <path d="M9 22.5v-6h6v6"></path>
    </svg>`,
  user: `
    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" stroke="currentColor" stroke-width="2"
      stroke-linecap="round" stroke-linejoin="round" viewBox="0 0 24 24">
      <circle cx="12" cy="7" r="4"></circle>
      <path d="M5.5 21a6.5 6.5 0 0113 0"></path>
    </svg>`,
  cog: `
    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" stroke="currentColor" stroke-width="2"
      stroke-linecap="round" stroke-linejoin="round" viewBox="0 0 24 24">
      <circle cx="12" cy="12" r="3"></circle>
      <path d="M19.4 15a1.65 1.65 0 00.33 1.82l.06.06a2 2 0 01-2.83 2.83l-.06-.06a1.65 1.65 0 00-1.82-.33 1.65 1.65 0 00-1 1.51V21a2 2 0 01-4 0v-.09a1.65 1.65 0 00-1-1.51 1.65 1.65 0 00-1.82.33l-.06.06a2 2 0 01-2.83-2.83l.06-.06a1.65 1.65 0 00.33-1.82 1.65 1.65 0 00-1.51-1H3a2 2 0 010-4h.09a1.65 1.65 0 001.51-1 1.65 1.65 0 00-.33-1.82l-.06-.06a2 2 0 012.83-2.83l.06.06a1.65 1.65 0 001.82.33h.09a1.65 1.65 0 001-1.51V3a2 2 0 014 0v.09a1.65 1.65 0 001 1.51h.09a1.65 1.65 0 001.82-.33l.06-.06a2 2 0 012.83 2.83l-.06.06a1.65 1.65 0 00-.33 1.82v.09a1.65 1.65 0 001.51 1H21a2 2 0 010 4h-.09a1.65 1.65 0 00-1.51 1z"></path>
    </svg>`,
  logout: `
    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" stroke="currentColor" stroke-width="2"
      stroke-linecap="round" stroke-linejoin="round" viewBox="0 0 24 24">
      <path d="M17 16l4-4m0 0l-4-4m4 4H7"></path>
      <path d="M7 16v1a2 2 0 01-2 2H5a2 2 0 01-2-2V7a2 2 0 012-2h.01a2 2 0 012 2v1"></path>
    </svg>`,
};
</script>

<template>
  <Head title="Dashboard" />

  <AuthenticatedLayout>
    <div class="flex min-h-screen bg-gradient-to-br from-emerald-900 via-teal-900 to-cyan-900 text-white">
      <!-- Sidebar -->
      <nav
        :class="[
          'fixed inset-y-0 left-0 z-30 w-64 overflow-y-auto bg-emerald-800 bg-opacity-90 backdrop-blur-md shadow-lg transform transition-transform duration-300 ease-in-out',
          sidebarOpen ? 'translate-x-0' : '-translate-x-full',
          'sm:translate-x-0 sm:static sm:inset-auto',
        ]"
      >
        <div class="p-6 flex flex-col h-full">
          <div class="mb-8 flex items-center space-x-3">
            <div
              class="h-12 w-12 rounded-full bg-gradient-to-r from-emerald-400 to-teal-400 flex items-center justify-center"
            >
              <svg class="h-6 w-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M12 11c0 3-1.5 5-4.5 5s-4.5-2-4.5-5 2-5 4.5-5 4.5 2 4.5 5zM15 7h1m-1 6h1m-4-4h1m-1 6h1"
                />
              </svg>
            </div>
            <span class="text-xl font-semibold">Mon App</span>
          </div>

          <ul class="flex-1 space-y-4">
            <li v-for="link in links" :key="link.name">
              <a
                :href="link.href"
                class="flex items-center space-x-3 rounded-lg px-4 py-3 hover:bg-emerald-600 transition-colors"
              >
                <span v-html="icons[link.icon]" class="flex-shrink-0"></span>
                <span class="font-medium">{{ link.name }}</span>
              </a>
            </li>
          </ul>

          <p class="mt-auto text-xs text-emerald-300">© 2025 Mon App. Tous droits réservés.</p>
        </div>
      </nav>

      <!-- Main content -->
      <div class="flex-1 flex flex-col">
        <!-- Top bar -->
        <header
          class="flex items-center justify-between bg-white/10 backdrop-blur-lg px-6 py-4 shadow-sm text-gray-900"
        >
          <button
            @click="sidebarOpen = !sidebarOpen"
            class="sm:hidden text-emerald-400 hover:text-emerald-300 focus:outline-none"
            aria-label="Toggle sidebar"
          >
            <svg
              v-if="!sidebarOpen"
              xmlns="http://www.w3.org/2000/svg"
              class="h-6 w-6"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
              viewBox="0 0 24 24"
            >
              <path d="M4 6h16M4 12h16M4 18h16" />
            </svg>
            <svg
              v-else
              xmlns="http://www.w3.org/2000/svg"
              class="h-6 w-6"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
              viewBox="0 0 24 24"
            >
              <path d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>

          <h1 class="text-xl font-semibold">Dashboard</h1>
          <div></div> <!-- Placeholder for right side, ex: user avatar -->
        </header>

        <!-- Page content -->
        <main class="flex-1 overflow-y-auto p-8">
          <h2 class="text-2xl font-semibold mb-6 text-white">Bienvenue dans votre tableau de bord !</h2>
          <p class="text-gray-200">
            Vous êtes connecté. Ici vous pouvez gérer vos paramètres, voir vos infos, etc.
          </p>
          <!-- Ici tu peux ajouter plus de contenu dynamique -->
        </main>
      </div>
    </div>
  </AuthenticatedLayout>
</template>

<style scoped>
/* Ajoute ici si tu veux customiser plus */
</style>
