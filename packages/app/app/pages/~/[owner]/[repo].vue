<script setup lang="ts">
import { computed } from "vue";

definePageMeta({
  name: "repo:details",
});

const route = useRoute();
const { data } = await useFetch("/api/repo", {
  query: computed(() => ({
    owner: route.params.owner,
    repo: route.params.repo,
  })),
});

if (!data.value) {
  throw createError("Could not load Repository");
}

const repository = data.value;

useHead({
  link: [
    { rel: "icon", href: "/favicon.png" },
    { rel: "icon", type: "image/svg+xml", href: "/favicon.svg" },
  ],
});
useSeoMeta({
  title: `${repository.owner.login}/${repository.name} Continuous Releases`,
  description: `See all ${repository.name} recent continuous releases.`,
  ogTitle: `${repository.owner.login}/${repository.name} Continuous Releases`,
  ogDescription: `See all ${repository.name} recent continuous releases.`,
});
// TODO: OG Image
</script>

<template>
  <div class="space-y-6">
    <div class="flex flex-col items-center gap-2">
      <a :href="repository.url" target="_blank">
        <UAvatar
          :src="repository.owner.avatarUrl"
          :alt="repository.name"
          size="xl"
          :ui="{
            root: 'rounded-md',
            image: 'rounded-md',
          }"
        />
      </a>
      <h1 class="text-2xl sm:text-3xl text-center">
        <a :href="repository.url" target="_blank">
          {{ repository.owner.login }}
          <span class="opacity-50">/</span>
          {{ repository.name }}
        </a>
      </h1>
      <div
        class="flex items-center justify-center gap-2 text-gray-700 dark:text-gray-300"
      >
        <UButton
          :to="repository.url"
          external
          target="_blank"
          :aria-label="`${repository.name}'s GitHub Repository`"
          icon="i-ph-github-logo"
          color="neutral"
          variant="link"
        />
        <UButton
          v-if="repository.homepageUrl"
          :to="repository.homepageUrl"
          external
          target="_blank"
          :aria-label="`${repository.name}'s Homepage`"
          icon="i-ph-globe-simple"
          color="neutral"
          variant="link"
        />
      </div>

      <div class="flex flex-col items-center justify-center mt-2">
        <p class="text-sm mb-[10px]">
          You can copy the badge and add it to your README!
        </p>
        <BadgeGenerator
          :owner="repository.owner.login"
          :repo="repository.name"
        />
      </div>
    </div>

    <Commits :owner="repository.owner.login" :repo="repository.name" />
  </div>
</template>
