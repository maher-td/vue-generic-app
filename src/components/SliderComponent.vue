<template>
    <section class="generic-slider">
        <swiper ref="awesomeSwiperGeneric" :options="swiperOptionGeneric">
            <swiper-slide v-bind:key="index" v-for="(item, index) in 5">
            <div class="generic-slider__details">
                <div class="generic-slider__img">
                <img src="https://picsum.photos/id/320/1024/768" />
                </div>
                <div class="generic-slider__caption">
                <h4>Classic Credit Card Banque misr offers</h4>
                <p>Credit limit starting from EGP 100000000</p>
                </div>
            </div>
            </swiper-slide>
        </swiper>
    </section>
</template>

<style lang="scss">
    $start: left;
    $end: right;

    .generic-slider {
    padding: 120px 60px;
    .swiper-slide {
        padding: 2px 0 10px;
        .generic-slider__details {
        display: flex;
        flex-direction: column;
        background-color: #fff;
        padding: 20px;
        box-shadow: 0 3px 6px 0 rgba(0, 0, 0, 0.16);
        .generic-slider__img {
            margin-bottom: 30px;
            width: 100%;
            position: relative;
            &:before {
            display: block;
            content: "";
            width: 100%;
            padding-top: (329 / 526) * 100%;
            }
            img {
            width: 100%;
            height: 100%;
            position: absolute;
            top: 0;
            right: 0;
            bottom: 0;
            left: 0;
            }
        }
        .generic-slider__caption {
            h3 {
            font-size: calc(
                14px + (34 - 14) * ((100vw - 768px) / (1920 - 768))
            );
            font-weight: bold;
            color: red;
            margin-bottom: 20px;
            }
            h4 {
            font-size: calc(
                14px + (24 - 14) * ((100vw - 768px) / (1920 - 768))
            );
            font-weight: bold;
            color: #000;
            margin-bottom: 30px;
            }
            p {
            font-size: calc(
                12px + (21 - 12) * ((100vw - 768px) / (1920 - 768))
            );
            margin-bottom: 30px;
            }
        }
        }
    }
    }
</style>

<script>
import { Swiper, SwiperSlide } from "vue-awesome-swiper";

export default {
    components: {
        Swiper,
        SwiperSlide
    },
    data: function() { 
      return {
       swiperOptionGeneric: {
        pagination: {
          el: ".swiper-pagination",
          dynamicBullets: true,
          clickable: true,
        },
        navigation: {
          nextEl: ".swiper-button-next",
          prevEl: ".swiper-button-prev",
        },
        loop: false,
        slidesPerView: 4,
        spaceBetween: 30,
        allowTouchMove: true,
        centeredSlides: false,
        breakpoints: {
          768: {
            slidesPerView: 4,
            spaceBetween: 20
          },
          500: {
            slidesPerView: 1.08,
            spaceBetween: 10,
            centeredSlides: true
          },
        },
      },
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
    },
    methods: {},
    computed: {},
    mounted() {
      // Reinit Slider

      this.$refs.awesomeSwiperGeneric.destroySwiper();
      this.$refs.awesomeSwiperGeneric.initSwiper();

    }
}
</script>