<script lang="ts" setup>
useHead({
  title: `Arslan's Projects`,
})

definePageMeta({
  name: 'Projects',
})
/**
 * projects 1st argument:
 * key: a unique key to ensure that data fetching can be properly de-duplicated across requests.
 * If you do not provide a key, then a key that is unique to the file name and line number of
 * the instance of useAsyncData will be generated for you.
 *
 */
const { data: projects } = await useAsyncData('projects', () => queryContent('projects').find())
</script>

<template>
  <div
    class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8 px-4 sm:px-12 justify-center"
  >
    <template v-for="project in projects" :key="project.title">
      <NuxtLink :to="`/projects/${project.slug}`" class="min-h-[250px]">
        <!-- project card  -->
        <div
          class="flex flex-col gap-2 w-auto p-4 cursor-pointer h-full rounded-md shadow hover:shadow-md text-slate-800 dark:text-white dark:bg-slate-800"
        >
          <div class="text-lg font-primary font-semibold">{{ project.title }}</div>
          <div class="text-sm flex-1 font-primary">{{ project.description }}</div>
          <div class="flex flex-col gap-2 justify-start items-start">
            <a
              v-if="project.projectUrl"
              class="text-xs text-pretty break-all hover:underline hover:cursor-pointer font-primary font-medium"
              @click.stop="null"
              :href="project.projectUrl"
              target="_blank"
              >{{ project.projectUrl }}</a
            >
            <a
              v-if="project.repoUrl"
              class="text-xs text-pretty break-all hover:underline hover:cursor-pointer font-primary font-medium"
              @click.stop="null"
              :href="project.repoUrl"
              target="_blank"
              >{{ project.repoUrl }}</a
            >
          </div>
        </div>
      </NuxtLink>
    </template>
  </div>
</template>

<style lang="css" scoped></style>
