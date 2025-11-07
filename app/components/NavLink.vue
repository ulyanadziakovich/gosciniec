<template>
  <NuxtLink
    v-if="isRouterLink"
    :to="routePath"
    class="nav-link-wrapper"
  >
    {{ value }}
  </NuxtLink>
  <a
    v-else
    :href="anchorPath"
    class="nav-link-wrapper"
  >
    {{ value }}
  </a>
</template>

<script setup lang="ts">
import { computed } from 'vue';

interface Props {
  value: string;
}

const props = defineProps<Props>();

const valueLower = computed(() => (props.value || '').toLowerCase().normalize('NFD').replace(/[\u0300-\u036f]/g, ''));

// robust route detection by substring (handles literówki i dodatkowe spacje)
const routePath = computed(() => {
  const v = valueLower.value.replace(/\s+/g, ' ').trim();

  if (v.includes('regulamin') || v.includes('regukamin')) return '/regulamin';
  if (v.includes('domek')) return '/domek';
  if (v.includes('go') && v.includes('sciniec')) return '/caly-teren'; // fuzzy check for gościniec variants
  if (v.includes('gosciniec') || v.includes('goscyniec')) return '/caly-teren';
  if (v.includes('pokoje')) return '/pokoje';
  if (v.includes('blog')) return '/blog';

  return '/';
});

const isRouterLink = computed(() => routePath.value !== '/');

const anchorPath = computed(() => {
  const v = valueLower.value.replace(/\s+/g, ' ').trim();
  if (v === 'okolica') return '#udogodnienia';
  return `#${v.replace(/\s+/g, '-')}`;
});
</script>

<style scoped>
.nav-link-wrapper {
  display: inline-block;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 1.3rem;
  line-height: normal;
  height: auto;
  white-space: normal;
  text-shadow: 2px 2px 4px #af4c1e, 3px 3px 6px #000000;
}
</style>
