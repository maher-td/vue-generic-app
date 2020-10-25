<template>
    <div id="app">
        <fontResizeAndColorInverter />
        <GallerySliderComponent />
        <SliderComponent />
        <ListingPageComponent />
    </div>
</template>

<script>
    import fontResizeAndColorInverter from './components/FontResizeAndColorInverterComponent.vue'
    import GallerySliderComponent from './components/GallerySliderComponent.vue'
    import SliderComponent from './components/SliderComponent.vue'
    import ListingPageComponent from './components/ListingPageComponent.vue'

    export default {
        name: 'App',
        components: {
            fontResizeAndColorInverter,
            GallerySliderComponent,
            SliderComponent,
            ListingPageComponent
        }
    }
</script>
