<script setup lang="ts">
import { ref, reactive } from "vue";
import { Swiper, SwiperSlide } from "swiper/vue";
import { Thumbs } from "swiper/modules";
import type { Swiper as SwiperInstance } from "swiper/types";

// 轮播数据
interface SlideItem {
  title: string;
  desc: string;
  color: string;
}

const slides: SlideItem[] = [
  { title: "Slide 1", desc: "Description for slide 1", color: "#4CAF50" },
  { title: "Slide 2", desc: "Description for slide 2", color: "#2196F3" },
  { title: "Slide 3", desc: "Description for slide 3", color: "#FF5722" },
  { title: "Slide 4", desc: "Description for slide 4", color: "#9C27B0" },
  { title: "Slide 5", desc: "Description for slide 5", color: "#FFC107" },
  { title: "Slide 6", desc: "Description for slide 6", color: "#3F51B5" },
  { title: "Slide 7", desc: "Description for slide 7", color: "#009688" },
  { title: "Slide 8", desc: "Description for slide 8", color: "#FFEB3B" },
];

// Swiper 实例
const mainSwiper = ref<SwiperInstance | null>(null);
const tabsSwiper = ref<SwiperInstance | null>(null);
const activeIndex = ref<number>(0);

// 事件：更新 activeIndex
const handleSlideChange = (swiper: SwiperInstance) => {
  activeIndex.value = swiper.activeIndex;
};

// Swiper 配置
const swiperOptions = reactive({
  modules: [Thumbs],
  speed: 300,
  thumbs: { swiper: tabsSwiper },
  onSwiper: (swiper: SwiperInstance) => (mainSwiper.value = swiper),
  onSlideChange: handleSlideChange,
});

const tabsSwiperOptions = reactive({
  modules: [Thumbs],
  slidesPerView: 5.5,
  onSwiper: (swiper: SwiperInstance) => (tabsSwiper.value = swiper),
  onClick: (swiper: SwiperInstance) => {
    if (swiper.clickedIndex !== undefined) {
      mainSwiper.value?.slideTo(swiper.clickedIndex);
    }
  },
});
</script>

<template>
  <div class="h-full flex flex-col">
    <!-- 头部 tab -->
    <div class="h-10 mb-2 bg-yellow">
      <Swiper
        v-bind="tabsSwiperOptions"
        class="h-full">
        <SwiperSlide
          v-for="(_, index) in slides"
          :key="'thumb-' + index">
          <div
            class="flex justify-center items-center h-full text-gray"
            :class="{ 'text-gray-8 font-bold': activeIndex === index }">
            {{ index + 1 }}
          </div>
        </SwiperSlide>
      </Swiper>
    </div>

    <!-- 主 Swiper -->
    <div class="flex-1 overflow-auto">
      <Swiper
        v-bind="swiperOptions"
        class="h-full">
        <SwiperSlide
          v-for="(slide, index) in slides"
          :key="index">
          <div
            class="h-full flex flex-col justify-center items-center"
            :style="{ backgroundColor: slide.color }">
            <div class="text-lg font-bold">{{ slide.title }}</div>
            <div class="text-sm">{{ slide.desc }}</div>
          </div>
        </SwiperSlide>
      </Swiper>
    </div>
  </div>
</template>
<style>
@import "swiper/css";
</style>
