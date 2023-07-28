<template>
    <div>
        <slot :currentSlide="currentSlide"></slot>
    </div>

    <!-- navigation -->
    <div v-if="navigationEnabled" class="navigation">
        <div class="toggle-page left">
            <i class="fa-solid fa-chevron-left" @click="leftSlide"></i>
        </div>

        <div class="toggle-page right">
            <i class="fa-solid fa-chevron-right"  @click="rightSlide"></i>
        </div>
    </div>

    <!-- pagination -->
    <div v-if="paginationEnabled" class="pagination">
        <span
         v-for="(slide,index) in getSlideCount"
         :key="index"
         :class="{active: index + 1 === currentSlide}"
         @click="goToSlide(index + 1)"
         >
        </span>
    </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';

const getSlideCount = ref(null);
const props = defineProps(['navigation','pagination','startAutoPlay','timeout']);
const autoPlayEnabled = ref(props.startAutoPlay === undefined ? true : props.startAutoPlay);
const timeoutDuration = ref(props.timeout === undefined ? 5000 : props.timeout);
const navigationEnabled = ref(props.navigation === undefined ? true : props.navigation);
const paginationEnabled = ref(props.pagination === undefined ? true : props.pagination);
const currentSlide = ref(1);


const rightSlide = () =>{
    if(currentSlide.value == getSlideCount.value){
        currentSlide.value = 1;
        return;
    }else{
        currentSlide.value++;
    }
}


const leftSlide = () =>{
    if(currentSlide.value == 1){
        currentSlide.value = getSlideCount.value;
        return;
    }else{
        currentSlide.value--;
    }
}
const autoPlay = () =>{
    setInterval(() => {
        rightSlide();
    },timeoutDuration.value);
}
onMounted(() =>{
    getSlideCount.value = document.querySelectorAll('.slide').length;
});

if(autoPlayEnabled.value){
    autoPlay();
}

const goToSlide = (slider) =>{
    currentSlide.value = slider;

}




</script>

<style scoped>

.navigation{
    position: absolute;
    display: flex;
    padding: 0 10px;
    justify-content: center;
    align-content: center;
    width: 100%;
    top: 50%;
}

.toggle-page{
    display: flex;
    flex: 1;
    cursor: pointer;
}

.right{
    justify-content: flex-end;
}

i{
    justify-content: center;
    align-items: center;
    display: flex;
    color: #fff;
    background-color: #6446d0;
    border-radius: 50%;
    width: 40px;
    height: 40px;
}

i:hover{
    background-color: #563cb6;
}

.pagination{
    position: absolute;
    display: flex;
    gap: 16px;
    justify-content: center;
    align-items: center;
    bottom: 24px;
    width: 100%;
}

span{
    background-color: #fff;
    height: 20px;
    width: 20px;
    border-radius: 50%;
    cursor: pointer;

}

.active{
    background-color: #6446d0;
}

</style>