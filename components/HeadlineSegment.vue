<script setup>
const props = defineProps({ headlineSegment: Object });

/** Storyblok "primary-highlight" is the brand accent (e.g. buttons); in headlines it must not recolor body text. */
const segmentClass = computed(() => {
  const highlight = props.headlineSegment?.highlight;
  if (highlight === 'primary-highlight') {
    return 'font-semibold text-inherit underline decoration-2 underline-offset-[0.15em] decoration-[var(--primary-highlight)]';
  }
  return `text-${highlight}`;
});
</script>

<template>
  <span v-editable="headlineSegment" :class="segmentClass">{{ headlineSegment.text }}</span>
</template>
