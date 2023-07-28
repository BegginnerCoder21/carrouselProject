<template>
    <div class="home">
        <Carousel 
            :navigation="true"
            :pagination="true"
            :startAutoPlay="true"
            :timeout="2000"
            class="carousel" 
            v-slot="{currentSlide}"
        >
            <Slide v-for="(slide,index) in carouselSlide" :key="index">
                <div  v-show="currentSlide === index + 1" class="slide-info"> 
                    <img :src="getImagepath(slide)" alt="" class="imageSlide">
                </div>
            </Slide>
        </Carousel>
    </div>
</template>

<script setup>
import Slide from '../Slide.vue';
import Carousel from '../carousel.vue';

const carouselSlide = ['bg-1','bg-2','bg-3'];

const getImagepath = (slide) => {
    return new URL(`../../assets/${slide}.jpg`, import.meta.url).pathname;
}

</script>

<style scoped>

.carousel{
    position: relative;
    max-height: 100vh;
    height: 100vh;

    
}
.slide-info{
    position: absolute;
    top: 0%;
    left: 0%;
    width: 100%;
    max-height: 100%;
    height: 100%;
}

.imageSlide{
    min-width: 100%;
    height: 100%;
    object-fit: cover;

}


</style>