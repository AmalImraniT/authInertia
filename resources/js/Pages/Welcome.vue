<script setup>
import { Head, Link } from '@inertiajs/vue3';

defineProps({
    canLogin: Boolean,
    canRegister: Boolean,
    appVersion: {
      type: String,
      required: true,
    },
});

function handleImageError() {
    document.getElementById('screenshot-container')?.classList.add('!hidden');
    document.getElementById('docs-card')?.classList.add('!row-span-1');
    document.getElementById('docs-card-content')?.classList.add('!flex-row');
    document.getElementById('background')?.classList.add('!hidden');
}
</script>

<template>
  <Head title="Bienvenue sur mon site" />
  <div class="bg-gray-50 text-black/70 dark:bg-black dark:text-white/60 min-h-screen relative">
    <!-- Background personnalisé -->
    <img
      id="background"
      class="absolute -left-20 top-0 max-w-[877px] opacity-20"
      src="/images/mon-background-personnalise.svg"
      alt="Background"
    />

    <div
      class="relative flex flex-col items-center justify-center min-h-screen selection:bg-[#FF2D20] selection:text-white"
    >
      <header class="grid grid-cols-2 items-center gap-2 py-10 lg:grid-cols-3 w-full max-w-7xl px-6">
        <!-- Logo ou nom -->
        <div class="flex justify-center lg:col-start-2">
          <h1 class="text-4xl font-bold text-[#FF2D20]">Amal Taibi</h1>
        </div>

        <!-- Navigation login/register -->
        <nav v-if="canLogin" class="-mx-3 flex flex-1 justify-end gap-2">
          <Link
            v-if="$page.props.auth.user"
            :href="route('dashboard')"
            class="rounded-md px-3 py-2 text-black hover:text-[#FF2D20] dark:text-white dark:hover:text-[#FF2D20]"
          >
            Tableau de bord
          </Link>

          <template v-else>
            <Link
              :href="route('login')"
              class="rounded-md px-3 py-2 text-black hover:text-[#FF2D20] dark:text-white dark:hover:text-[#FF2D20]"
            >
              Connexion
            </Link>

            <Link
              v-if="canRegister"
              :href="route('register')"
              class="rounded-md px-3 py-2 text-black hover:text-[#FF2D20] dark:text-white dark:hover:text-[#FF2D20]"
            >
              Inscription
            </Link>
          </template>
        </nav>
      </header>

      <main class="mt-6 w-full max-w-7xl px-6 grid gap-6 lg:grid-cols-2 lg:gap-8">
        <!-- Carte personnalisée -->
        <a
          href="https://ton-site.com/documentation"
          id="docs-card"
          class="flex flex-col items-start gap-6 rounded-lg bg-white p-6 shadow-md ring-1 ring-gray-200 hover:ring-[#FF2D20] transition dark:bg-zinc-900 dark:ring-zinc-800 dark:hover:ring-[#FF2D20]"
        >
          <div
            id="screenshot-container"
            class="relative flex w-full flex-1 items-stretch rounded-md overflow-hidden"
          >
            <img
              src="/images/mon-doc-screenshot.png"
              alt="Screenshot documentation"
              class="aspect-video w-full object-cover"
              @error="handleImageError"
            />
          </div>

          <div
            id="docs-card-content"
            class="flex items-center gap-6 lg:flex-col"
          >
            <div class="flex shrink-0 items-center justify-center rounded-full bg-[#FF2D20]/10 p-4">
              <svg
                class="w-6 h-6 text-[#FF2D20]"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M12 8v4l3 3"
                />
              </svg>
            </div>

            <div>
              <h2 class="text-xl font-semibold text-black dark:text-white">
                Documentation
              </h2>
              <p class="mt-2 text-sm leading-relaxed">
                Découvrez toute la documentation de mon projet pour bien
                démarrer et utiliser toutes les fonctionnalités.
              </p>
            </div>
          </div>
        </a>

        <!-- Autres liens / ressources -->
        <a
          href="https://ton-site.com/tutoriels"
          class="flex items-start gap-4 rounded-lg bg-white p-6 shadow-md ring-1 ring-gray-200 hover:ring-[#FF2D20] transition dark:bg-zinc-900 dark:ring-zinc-800 dark:hover:ring-[#FF2D20]"
        >
          <div class="flex shrink-0 items-center justify-center rounded-full bg-[#FF2D20]/10 p-4">
            <svg
              class="w-6 h-6 text-[#FF2D20]"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M14.25 10.5l-3 3m0 0l-3-3m3 3v-6"
              />
            </svg>
          </div>

          <div>
            <h2 class="text-xl font-semibold text-black dark:text-white">
              Tutoriels
            </h2>
            <p class="mt-2 text-sm leading-relaxed">
              Apprenez étape par étape à maîtriser toutes les facettes de mon
              projet.
            </p>
          </div>
        </a>
      </main>

      <footer class="py-16 text-center text-sm text-black/50 dark:text-white/50">
        Version de l'application v{{ appVersion }} — Développé par Amal Taibi
      </footer>
    </div>
  </div>
</template>
