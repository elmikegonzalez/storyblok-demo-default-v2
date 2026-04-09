<script setup>
const props = defineProps({ headlineSegment: Object });

const segmentClass = computed(() => {
  const highlight = props.headlineSegment?.highlight;
  if (!highlight || highlight === 'primary-highlight') {
    return '';
  }
  return `text-${highlight}`;
});
</script>

<template>
  <span v-editable="headlineSegment" :class="segmentClass">{{ headlineSegment.text }}</span>
</template>
