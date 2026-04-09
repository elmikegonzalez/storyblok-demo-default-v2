<script setup>
const props = defineProps({ blok: Object, index: Number, referenced: Boolean });

const showVideo = computed(() => {
  return Boolean(props.blok.background_video?.filename);
});

const overlay = computed(() => showVideo.value);
</script>

<template>
  <section
    v-editable="blok"
    class="page-section banner-section relative flex min-h-[600px] items-center overflow-hidden"
    :class="[`bg-${blok?.background_color}`]"
  >
    <div class="container relative z-20 flex" :class="[{ 'justify-center text-center': blok.text_alignment === 'center' }, { 'text-white': overlay }]">
      <div class="relative z-30 max-w-3xl">
        <Headline v-if="blok.headline" :index="index" :headline="blok.headline" :color="overlay ? 'text-white' : ''" />
        <Lead v-if="blok.lead">{{ blok.lead }}</Lead>
        <div v-if="blok?.buttons?.length" class="flex flex-col gap-4 sm:flex-row" :class="blok.text_alignment === 'center' ? 'justify-center' : 'justify-start items-start'">
          <Button
            v-for="button in blok.buttons"
            :key="button._uid"
            :button="button"
          />
        </div>
      </div>
    </div>
    <div v-if="overlay" class="absolute left-0 top-0 z-10 size-full bg-black/30"></div>
    <video
      v-if="showVideo"
      :src="blok.background_video.filename"
      :alt="blok.background_video.alt"
      class="absolute left-0 top-0 z-0 size-full object-cover"
      autoplay
      muted
      loop
    ></video>
  </section>
</template>
