<template>
    <div class="carousel__btn-container">
        <button 
            class="carousel__btn" 
            @click="selectedBtn(0)"
            :class="{selected: currentIndex === 0}"></button>

        <button 
            class="carousel__btn" 
            @click="selectedBtn(1)"
            :class="{selected: currentIndex === 1}"></button>

        <button 
            class="carousel__btn" 
            @click="selectedBtn(2)"
            :class="{selected: currentIndex === 2}"></button>

        <button 
            class="carousel__btn__tablet" 
            @click="selectedBtn(3)"
            :class="{selected: currentIndex === 3}"></button>

        <button 
            class="carousel__btn__tablet" 
            @click="selectedBtn(4)"
            :class="{selected: currentIndex === 4}"></button>
    </div>
</template>

<script>
export default {
    props: {
        currentIndex: {
            type: Number,
            default: 0
        }
    },
    methods: {
        selectedBtn(index) {
            this.$emit('selected-btn', index)
        }
    }
}
</script>

<style lang="scss" scoped>
.carousel__btn-container {
    display: flex;
    gap: 10px;
}

.carousel__btn,
.carousel__btn__tablet {
    width: 16px;
    height: 16px;
    border-radius: 50px;
    border: none;
    background: $dark;
    cursor: pointer;
    transition: background 0.3s ease-in-out;

    &.selected {
        background: $sand;
    }
}

.carousel__btn__tablet {
    display: none;

    @include tablet {
        display: block;
    }
}
</style>