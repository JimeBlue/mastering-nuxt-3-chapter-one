<template>
  <h2>Lesson</h2>
  <p>This is a lesson</p>
  <p>{{ chapter.title }}</p>
  <p>{{ lesson.title }}</p>
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
</script>
