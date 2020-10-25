<template>
    <div id="app">
        <FontResizeAndColorInverter />
        <SocialMediaComponent />
        <FormValidationVuelidate />
        <GallerySliderComponent />
        <SliderComponent />
        <AosAnimationComponent />
        <ListingPageComponent />
    </div>
</template>

<style lang="scss">
    @import '../src/assets/sass/IEDisclaimerStyle';
</style>

<script>
    import FontResizeAndColorInverter from './components/FontResizeAndColorInverterComponent.vue'
    import SocialMediaComponent from './components/SocialMediaComponent.vue'
    import FormValidationVuelidate from './components/FormValidationVuelidate.vue'
    import GallerySliderComponent from './components/GallerySliderComponent.vue'
    import SliderComponent from './components/SliderComponent.vue'
    import AosAnimationComponent from './components/AosAnimationComponent.vue'
    import ListingPageComponent from './components/ListingPageComponent.vue'

    export default {
        name: 'App',
        components: {
            FontResizeAndColorInverter,
            SocialMediaComponent,
            FormValidationVuelidate,
            GallerySliderComponent,
            SliderComponent,
            AosAnimationComponent,
            ListingPageComponent
        }
    }
</script>
