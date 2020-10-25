<template>
  <div id="app">
    <GallerySliderComponent/>
    <SliderComponent/>
    <ListingPageComponent/>
  </div>
</template>

<script>
import GallerySliderComponent from './components/GallerySliderComponent.vue'
import SliderComponent from './components/SliderComponent.vue'
import ListingPageComponent from './components/ListingPageComponent.vue'

export default {
  name: 'App',
  components: {
    GallerySliderComponent,
    SliderComponent,
    ListingPageComponent
  }
}
</script>
