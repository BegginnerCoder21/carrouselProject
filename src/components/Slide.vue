<template>
    <div class="slide">
        <Transition name="slide">
            <slot ></slot>
        </Transition>
    </div>
</template>

<script setup>

</script>

<style scoped>

.slide-leave-active,
.slide-enter-active{
    transition: .7s ease-in-out all;
}

.slide-leave-to,
.slide-enter-from{
    opacity: 0;
}

.slide-enter-to,
.slide-leave-from{
    opacity: 1;
}

</style>