<script setup>
const props = defineProps({ headlineSegment: Object });

const isPrimaryHighlight = computed(() => props.headlineSegment?.highlight === 'primary-highlight');

const segmentClass = computed(() => {
  if (isPrimaryHighlight.value) {
    return 'headline-segment--accent';
  }
  return `text-${props.headlineSegment?.highlight}`;
});
</script>

<template>
  <span v-editable="headlineSegment" :class="segmentClass">{{ headlineSegment.text }}</span>
</template>

<style scoped>
.headline-segment--accent {
  color: inherit;
  font-weight: 600;
  text-decoration: underline;
  text-decoration-color: var(--primary-highlight);
  text-decoration-thickness: 2px;
  text-underline-offset: 0.15em;
}
</style>
