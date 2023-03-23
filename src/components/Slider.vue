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
      <Transition name="thumb-fade">
        <picture v-show="loaded" class="slider__thumb__picture">
          <source :srcset="imgSet[currentIndex || 0].thumbSrcset" type="image/jpg" />
          <img
            :srcset="imgSet[currentIndex || 0].thumbSrcset"
            type="image/jpg"
            alt="Carousel image"
            class="slider__thumb__img"
          />
        </picture>
      </Transition>
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
  loaded = ref(true)

let autoPlayTimeout = null

const changeImg = () => {
  loaded.value = false
  
  // Increas slider index and show fade in/fade out animation
  setTimeout(() => {
    loaded.value = !loaded.value
    currentIndex.value === imgSet.length - 1 ? stopAutoPlay() : currentIndex.value += 1
  }, 400)

  // Start of the slider
  startAutoPlay()
}

// Start the slider and loop every 8 sec
const startAutoPlay = () => {
  autoPlayTimeout = setTimeout(() => {
    changeImg()
  }, 8000)
}

// After iteration through all images, stop the slider
const stopAutoPlay = () => {
  clearTimeout(autoPlayTimeout)
  currentIndex.value = 0
}
</script>
