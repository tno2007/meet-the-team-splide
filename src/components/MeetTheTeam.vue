<script setup lang="ts">
import { Splide } from "@splidejs/splide";
import { onMounted, ref } from 'vue'
import { team } from "../data/team";

const props = defineProps({
    foo: String,
    bar: {
        type: Number,
        required: false
    }
})

onMounted(() => {
    var splide = new Splide(".splide", {
        type: "loop",
        focus: "center",
        //autoplay: true,
        //rewind: true,
        perPage: 3,
        //perMove: 1,
        trimSpace: false,
        keyboard: true,
        //width: "100vw",
        //height: "100vh",
        pagination: false,
        updateOnMove: true,
        //drag: false,
        waitForTransition: false,
    });
    splide.mount();
})

</script>

<style lang="scss">
@import "@splidejs/splide/dist/css/splide.min.css";

.block {
    background: #c0e900;
    background: linear-gradient(0deg, #98e228 20%, #c0e900);
    box-shadow: 1rem 1rem 30px 4px rgba(83, 137, 8, 0.1);
    width: 320px;
    height: 320px;
    opacity: 1;
    overflow: hidden;
    position: relative;

    transition: opacity 0.4s ease, -webkit-transform 0.4s ease-out;
    transition: transform 0.4s ease-out, opacity 0.4s ease;
    transition: transform 0.4s ease-out, opacity 0.4s ease,
        -webkit-transform 0.4s ease-out;

    will-change: transform;
}

.splide__slide {
    opacity: 0.3;

    .container {
        .description {
            bottom: 0;
            width: 100%;
            height: 80px;
            background: #fff;
            padding: 0.5em 1em;
            position: absolute;
            -webkit-transition: all, 0.45s ease;
            -moz-transition: all, 0.45s ease;
            -o-transition: all, 0.45s ease;
            transition: all, 0.45s ease;
        }
    }

    &.is-active {
        .container {
            .description {
                bottom: -80px;
            }
        }
    }
}

.splide__slide.is-active {
    opacity: 1;
}
</style>

<template>
    <div class="splide">
        <div class="splide__track">
            <ul class="splide__list">
                <li class="splide__slide" v-for="t in team">
                    <div class="container">
                        <img class="image" :src="`../src/assets/images/${t.imageUrl}`" />
                        <div class="description">
                            <div class="name">{{ t.name }}</div>
                            <div class="title">{{ t.title }}</div>
                        </div>
                    </div>
                </li>
            </ul>
        </div>
    </div>
</template>