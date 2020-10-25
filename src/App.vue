<template>
    <div id="app">
        <FontResizeAndColorInverter />
        <SocialMediaComponent />
        <GallerySliderComponent />
        <SliderComponent />
        <ListingPageComponent />
    </div>
</template>

<script>
    import FontResizeAndColorInverter from './components/FontResizeAndColorInverterComponent.vue'
    import SocialMediaComponent from './components/SocialMediaComponent.vue'
    import GallerySliderComponent from './components/GallerySliderComponent.vue'
    import SliderComponent from './components/SliderComponent.vue'
    import ListingPageComponent from './components/ListingPageComponent.vue'

    export default {
        name: 'App',
        components: {
            FontResizeAndColorInverter,
            SocialMediaComponent,
            GallerySliderComponent,
            SliderComponent,
            ListingPageComponent
        }
    }
</script>
