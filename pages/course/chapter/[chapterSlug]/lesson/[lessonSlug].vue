<template>
  <div>
    <p class="mt-0 uppercase font-bold text-slate-400 mb-1">
      Lesson {{ chapter.number }} - {{ lesson.number }}
    </p>
    <h2 class="my-0">{{ lesson.title }}</h2>
    <div class="flex space-x-4 mt-2 mb-8">
      <a
        v-if="lesson.sourceUrl"
        class="font-normal text-md text-gray-500"
        :href="lesson.sourceUrl"
      >
        Download Source Code
      </a>
      <a
        v-if="lesson.downloadUrl"
        class="font-normal text-md text-gray-500"
        :href="lesson.downloadUrl"
      >
        Download Video
      </a>
    </div>
    <VideoPlayer v-if="lesson.videoId" :videoId="lesson.videoId" />
    <p>{{ lesson.text }}</p>
  </div>
</template>
<script setup>
const course = useCourse();
const route = useRoute();

// search for the chapter in the useCourse composable which has a slug matching the
//chapterSlug route parameter
const chapter = computed(() => {
  return course.chapters.find(
    (chapter) => chapter.slug === route.params.chapterSlug,
  );
});

// Go to the current chapter and look for a lesson which has a slug matching the lessonSlug route parameter
const lesson = computed(() => {
  return chapter.value.lessons.find(
    (lesson) => lesson.slug === route.params.lessonSlug,
  );
});
// Calculated title of the page
const title = computed(() => {
  return `${lesson.value.title} - ${course.title}`;
});
useHead({
  title,
});
</script>
