<template>
  <div
    class="slider"
    :style="`--ambient-bg: url(${imgSet[currentIndex || 0].srcset.split(',')[0]})`"
  >
    <div class="slider__main">
      <Transition>
        <picture v-show="loaded" class="slider__main__picture">
          <source :srcset="imgSet[currentIndex || 0].srcset" type="image/jpg" />
          <img
            :srcset="imgSet[currentIndex || 0].srcset"
            type="image/jpg"
            alt="Carousel image"
            class="slider__main__img"
          />
        </picture>
      </Transition>
    </div>

    <div class="slider__thumb">
      <picture class="slider__thumb__picture">
        <source :srcset="imgSet[currentIndex || 0].thumbSrcset" type="image/jpg" />
        <img
          :srcset="imgSet[currentIndex || 0].thumbSrcset"
          type="image/jpg"
          alt="Carousel image"
          class="slider__thumb__img"
        />
      </picture>
    </div>

    <button @click="changeImg()" class="slider__btn" />

    <div class="slider__pagination">
      <div class="slider__pagination__item">
        <span
          class="slider__pagination__item__progress"
          :class="{ active: currentIndex === 0 }"
        ></span>
      </div>
      <div class="slider__pagination__item">
        <span
          class="slider__pagination__item__progress"
          :class="{ active: currentIndex === 1 }"
        ></span>
      </div>
      <div class="slider__pagination__item">
        <span
          class="slider__pagination__item__progress"
          :class="{ active: currentIndex === 2 }"
        ></span>
      </div>
      <div class="slider__pagination__item">
        <span
          class="slider__pagination__item__progress"
          :class="{ active: currentIndex === 3 }"
        ></span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue'

const imgSet = reactive([
  {
    srcset:
      'src/assets/img/carousel/carousel-photo-01.jpg, src/assets/img/carousel/carousel-photo-01@2x.jpg, src/assets/img/carousel/carousel-photo-01@3x.jpg',
    thumbSrcset:
      'src/assets/img/thumbnail/small-carousel-photo-04.jpg, src/assets/img/thumbnail/small-carousel-photo-04@2x.jpg, src/assets/img/thumbnail/small-carousel-photo-04@3x.jpg'
  },
  {
    srcset:
      'src/assets/img/carousel/carousel-photo-02.jpg, src/assets/img/carousel/carousel-photo-02@2x.jpg, src/assets/img/carousel/carousel-photo-02@3x.jpg',
    thumbSrcset:
      'src/assets/img/thumbnail/small-carousel-photo-01.jpg, src/assets/img/thumbnail/small-carousel-photo-01@2x.jpg, src/assets/img/thumbnail/small-carousel-photo-01@3x.jpg'
  },
  {
    srcset:
      'src/assets/img/carousel/carousel-photo-03.jpg, src/assets/img/carousel/carousel-photo-03@2x.jpg, src/assets/img/carousel/carousel-photo-03@3x.jpg',
    thumbSrcset:
      'src/assets/img/thumbnail/small-carousel-photo-02.jpg, src/assets/img/thumbnail/small-carousel-photo-02@2x.jpg, src/assets/img/thumbnail/small-carousel-photo-02@3x.jpg'
  },
  {
    srcset:
      'src/assets/img/carousel/carousel-photo-04.jpg, src/assets/img/carousel/carousel-photo-04@2x.jpg, src/assets/img/carousel/carousel-photo-04@3x.jpg',
    thumbSrcset:
      'src/assets/img/thumbnail/small-carousel-photo-03.jpg, src/assets/img/thumbnail/small-carousel-photo-03@2x.jpg, src/assets/img/thumbnail/small-carousel-photo-03@3x.jpg'
  }
])

const currentIndex = ref(null),
  loaded = ref(true),
  startAutoPlay = ref(false)

const changeImg = () => {
  loaded.value = false
  startAutoPlay.value = true

  if (currentIndex.value === imgSet.length - 1) {
    // Start slider loop and return to first image, start of the slide
    startAutoPlay.value = false
    setTimeout(() => {
      loaded.value = !loaded.value
      currentIndex.value = 0
    }, 400)
  } else {
    // Increas slider index and show fade in/fade out animation
    setTimeout(() => {
      loaded.value = !loaded.value
      currentIndex.value += 1
    }, 400)
  }

  let autoPlayTimeout = null
  if (startAutoPlay.value) {
    // Start the slider and loop every 8 sec
    autoPlayTimeout = setTimeout(() => {
      changeImg()
    }, 8000)
  } else {
    // After iteration through all images, stop the slider
    clearTimeout(autoPlayTimeout)
  }
}
</script>
