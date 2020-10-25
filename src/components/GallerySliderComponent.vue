<template>
  <section class="generic-gallery-slider">

    <CoolLightBox :items="imgArray"
    :index="fullScreenIndex"
    :effect="'fade'"
    :slideshow = 'false'
    :enableWheelEvent = 'true'
    ref="light"
    @on-change="changeEvent"
    @on-open="openEvent"
    @close="closeEvent"
  >
    </CoolLightBox>

    <div class="thumb-example">
      <swiper class="swiper gallery-top" :options="swiperOptionTop" ref="swiperTop">
          <swiper-slide class="main-slide" v-bind:key="index" v-for="(item, index) in imgArray">
              <div class="item">
                  <img :src="item.thumb" v-on:click="openFullScreen(index)" />
              </div>
          </swiper-slide>
      </swiper>

      <div class="slider-container">
          <div class="swiper-button-next" slot="button-next" v-show="isArrows">
              <i class="icon-right-arrow"></i>
          </div>
          <swiper class="swiper gallery-thumbs" :options="swiperOptionThumbs" ref="swiperThumbs">
              <swiper-slide class="thumb-slide" v-bind:key="index" :id="index" v-for="(item, index) in imgArray">
                  <div class="slider-thumb-img">
                      <div class="item">
                          <img :src="item.thumb" />
                      </div>
                      <div class="img-thumb">
                          <i class="icon-photo"></i>
                      </div>
                  </div>
              </swiper-slide>
          </swiper>
          <div class="swiper-button-prev" slot="button-prev" v-show="isArrows">
              <i class="icon-left-arrow"></i>
          </div>
      </div>
    </div>

  </section>
</template>

<style lang="scss">
$start: left;
$end: right;

.generic-gallery-slider {
  padding: 60px 300px;
  .thumb-example {
    background-color: #e6e2e2;

    .slider-container {
      position: relative;
      padding: 20px 0;
      background-color: #e6e2e2;
      height: 130px;

      .swiper-button-next,
      .swiper-button-prev {
        display: flex;
        align-items: center;
        justify-content: center;
        background-color: #f9f9f9;
        background-image: none !important;
        outline: none;
        height: 100%;
        width: 45px;
        top: 0;
        margin-top: 0;

        i {
          &:before {
            color: #787878;
            font-size: 12px;
          }
        }
      }

      .swiper-button-prev {
        border-top-right-radius: 20px;
        border-bottom-right-radius: 20px;
        left: 0;
      }

      .swiper-button-next {
        border-top-left-radius: 20px;
        border-bottom-left-radius: 20px;
        right: 0;
      }
    }

    .main-slide {
      position: relative;

      &:before {
        display: block;
        content: "";
        width: 100%;
        padding-top: (63 / 92) * 100%;
      }

      .item {
        position: absolute;
        top: 0;
        #{$start}: 0;
        bottom: 0;
        #{$end}: 0;
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;

        img {
          width: 100%;
          max-height: 100%;
        }
      }
    }

    .slider-video {
      &:before {
        display: none;
      }
    }
  }

  .swiper {
    .swiper-slide {
      background-size: cover;
      background-position: center;

      .video-item {
        width: 100%;
        height: 100%;

        iframe {
          width: 100%;
          height: 100%;
        }
      }

      .slider-thumb-img {
        position: relative;
        width: 100%;
        height: 100%;

        &:before {
          display: block;
          content: "";
          width: 100%;
          padding-top: (7 / 12) * 100%;
        }

        .item {
          position: absolute;
          top: 0;
          #{$start}: 0;
          bottom: 0;
          #{$end}: 0;
          width: 100%;
          height: 100%;
          display: flex;
          justify-content: center;
          align-items: center;

          img {
            max-width: 100%;
            max-height: 100%;
          }
        }

        .img-thumb {
          position: absolute;
          top: 0;
          width: 100%;
          height: 100%;
          background-color: #000000;
          opacity: 0.4;
          display: flex;
          justify-content: center;
          align-items: center;
          transition: 0.5s;

          .icon-youtube {
            &:before {
              color: #ffffff;
            }
          }

          &:hover {
            opacity: 0;
          }
        }
      }
    }

    &.gallery-top {
      height: 630px;
      width: 100%;
    }

    &.gallery-thumbs {
      height: 100%;
      box-sizing: border-box;
      margin: 0 auto;
      width: 90%;
    }

    &.gallery-thumbs .swiper-slide {
      width: 16%;
      height: 100%;
    }
  }
}
</style>

<script>
import { Swiper, SwiperSlide } from "vue-awesome-swiper";

import CoolLightBox from 'vue-cool-lightbox'
import 'vue-cool-lightbox/dist/vue-cool-lightbox.min.css'

let galleryThis;
let fullScreenOpen;
let fullScreenClose;

export default {
  name: 'HelloWorld',
  components: {
    Swiper,
    SwiperSlide,
    CoolLightBox
  },
    data: function() { 
      return {
      fullScreenIndex: null,
      imgArray: [
        {
        src: "https://picsum.photos/id/320/1024/768",
        thumb:"https://picsum.photos/id/320/1024/768",
        title: 'a beautiful mountain view 1',
        description: "Photo by Facundo 1",
        },
        {
        src: "https://picsum.photos/id/310/1024/768",
        thumb:"https://picsum.photos/id/310/1024/768",
        title: 'a beautiful mountain view 2',
        description: "Photo by Facundo 2",
        },
        {
        src: "https://picsum.photos/id/300/1024/768",
        thumb:"https://picsum.photos/id/300/1024/768",
        title: 'a beautiful mountain view 3',
        description: "Photo by Facundo 3",
        },
        {
        src: "https://picsum.photos/id/330/1024/768",
        thumb:"https://picsum.photos/id/330/1024/768",
        title: 'a beautiful mountain view 4',
        description: "Photo by Facundo 4",
        },
        {
        src: "https://picsum.photos/id/340/1024/768",
        thumb:"https://picsum.photos/id/340/1024/768",
        title: 'a beautiful mountain view 5',
        description: "Photo by Facundo 5",
        },
        {
        src: "https://picsum.photos/id/350/1024/768",
        thumb:"https://picsum.photos/id/350/1024/768",
        title: 'a beautiful mountain view 6',
        description: "Photo by Facundo 6",
        },
        {
          src: "https://www.youtube.com/embed/r6zIGXun57U",
          thumb:"https://picsum.photos/id/370/1024/768",
          title: 'Video',
          description: "Video",
          autoplay: true,
        },
        {
        src: "https://picsum.photos/id/360/1024/768",
        thumb:"https://picsum.photos/id/360/1024/768",
        title: 'a beautiful mountain view 7',
        description: "Photo by Facundo 7",
        }
      ],
      isArrows: true,
      swiperOptionTop: {
        loop: true,
        loopedSlides: 5, // looped slides should be the same
        spaceBetween: 10,
        allowTouchMove: true,
        threshold: 40,
        speed: 800,
        updateOnWindowResize: false,
        navigation: {
            nextEl: '.swiper-button-next',
            prevEl: '.swiper-button-prev'
        }
      },
      swiperOptionThumbs: {
        loop: true,
        loopedSlides: 5, // looped slides should be the same
        spaceBetween: 10,
        centeredSlides: true,
        slidesPerView: 6,
        touchRatio: 0.2,
        slideToClickedSlide: true,
        speed: 800,
        breakpoints: {
            500: {
                slidesPerView: 4,
            }
        }
      }
    }
    },
    methods: {
      openFullScreen(index) {
        galleryThis.fullScreenIndex = index;
      },
      changeEvent() {
        fullScreenClose = galleryThis.$refs.light.imgIndex
      },
      openEvent() {
        fullScreenOpen = galleryThis.fullScreenIndex
      },
      closeEvent() {

        galleryThis.fullScreenIndex = null

        if (fullScreenClose > fullScreenOpen) {
          for (let x = 0; x < fullScreenClose - fullScreenOpen; x++) {
            galleryThis.$refs.swiperTop.$swiper.slideNext(0);
          }
        } else if (fullScreenClose < fullScreenOpen) {
          for (let y = 0; y < fullScreenOpen - fullScreenClose; y++) {
            galleryThis.$refs.swiperTop.$swiper.slidePrev(0);
          }
        }

      }
    },
    computed: {},
    mounted() {
      // Reinit Slider

      galleryThis = this;

      // galleryThis.fullScreenIndex = 1;

      galleryThis.$nextTick(() => {
        let swiperTop = galleryThis.$refs.swiperTop.$swiper
        let swiperThumbs = galleryThis.$refs.swiperThumbs.$swiper
        swiperTop.controller.control = swiperThumbs
        swiperThumbs.controller.control = swiperTop
      })
    }
}
</script>