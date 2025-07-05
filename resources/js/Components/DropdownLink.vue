<script setup>
import { Link, Inertia } from '@inertiajs/vue3';
import { defineProps } from 'vue';

const props = defineProps({
  href: {
    type: String,
    required: true,
  },
  method: {
    type: String,
    default: 'get',
  },
  as: {
    type: String,
    default: 'a',
  },
});

const handleClick = (event) => {
  if (props.method.toLowerCase() === 'post') {
    event.preventDefault();
    Inertia.post(props.href);
  }
  // Tu peux gérer d’autres méthodes si besoin
};
</script>

<template>
  <component
    :is="props.as === 'button' ? 'button' : Link"
    :href="props.as === 'button' ? undefined : props.href"
    class="block w-full px-4 py-2 text-start text-sm leading-5 text-gray-700 transition duration-150 ease-in-out hover:bg-gray-100 focus:bg-gray-100 focus:outline-none"
    @click="handleClick"
  >
    <slot />
  </component>
</template>
