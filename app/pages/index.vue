<script setup lang="ts">
const { data: page } = await useAsyncData("index", () =>
  queryCollection("landing").path("/").first()
);
if (!page.value) {
  throw createError({
    statusCode: 404,
    statusMessage: "Page not found",
    fatal: true,
  });
}

const title = page.value.seo?.title || page.value.title;
const description = page.value.seo?.description || page.value.description;

useSeoMeta({
  titleTemplate: "",
  title,
  ogTitle: title,
  description,
  ogDescription: description,
  ogImage: "https://docs-template.nuxt.dev/social-card.png",
  twitterImage: "https://docs-template.nuxt.dev/social-card.png",
});
</script>

<template>
  <div>
    <UAlert
      description="Using the FormField wrapper"
      class="max-w-lg mx-auto mt-10"
      variant="subtle"
    />
    <div class="flex gap-2 justify-center mt-6 border border-muted">
      <UFormField label="search">
        <UInput type="search" class="w-28" />
      </UFormField>
      <UFormField label="text">
        <UInput type="text" class="w-28" />
      </UFormField>
      <UFormField label="select">
        <USelect class="w-28" />
      </UFormField>
    </div>
    <UAlert
      description="This group has removed the FormField wrapper"
      class="max-w-lg mx-auto mt-6"
      variant="subtle"
    />
    <div class="flex gap-2 justify-center mt-6 border-y border-muted">
      <UInput type="search" class="w-28" placeholder="search" />
      <UInput type="text" class="w-28" placeholder="text" />
      <USelect class="w-28" placeholder="select" />
    </div>
    <ContentRenderer v-if="page" :value="page" :prose="false" />
  </div>
</template>
