<template>
    <div id="app">
        <fontResizeAndColorInverter />
        <GallerySliderComponent />
        <AosAnimationComponent />
        <SliderComponent />
        <ListingPageComponent />
    </div>
</template>

<style lang="scss">
    @import '../src/assets/sass/IEDisclaimerStyle';
</style>


<script>
    import fontResizeAndColorInverter from './components/FontResizeAndColorInverterComponent.vue'
    import GallerySliderComponent from './components/GallerySliderComponent.vue'
    import AosAnimationComponent from './components/AosAnimationComponent.vue'
    import SliderComponent from './components/SliderComponent.vue'
    import ListingPageComponent from './components/ListingPageComponent.vue'

    export default {
        name: 'App',
        components: {
            fontResizeAndColorInverter,
            GallerySliderComponent,
            AosAnimationComponent,
            SliderComponent,
            ListingPageComponent
        }
    }
</script>
