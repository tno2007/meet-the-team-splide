<script setup lang="ts">
import { Splide } from "@splidejs/splide";
import { onMounted, ref } from "vue";
import { team } from "../data/team";

const props = defineProps({
    foo: String,
    bar: {
        type: Number,
        required: false,
    },
});

onMounted(() => {
    const list = new Splide("#thumbnail-list", {
        type: "loop",
        focus: "center",
        //autoplay: true,
        //rewind: true,
        perPage: 5,
        breakpoints: {
            640: {
                perPage: 2,
            },
        },
        //perMove: 1,
        trimSpace: false,
        keyboard: true,
        //width: "100vw",
        //height: "100vh",
        pagination: false,
        updateOnMove: true,
        //drag: false,
        waitForTransition: false,
        //isNavigation: true,
    });

    const detail = new Splide("#thumbnail-detail", {
        type: "fade",
        rewind: true,
        pagination: false,
        arrows: false,
    });

    list.sync(detail);
    list.mount();
    detail.mount();
});
</script>

<style lang="scss">
@import "@splidejs/splide/dist/css/splide.min.css";

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
                height: 0;
            }
        }
    }
}

.splide__slide.is-active {
    opacity: 1;
}
</style>

<template>
    <div>
        <div id="thumbnail-list" class="splide">
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
    </div>

    <div id="thumbnail-detail" class="splide">
        <div class="splide__track">
            <ul class="splide__list">
                <li class="splide__slide" v-for="t in team">
                    <div class="container">
                        <p v-html="t.description"></p>
                    </div>
                </li>
            </ul>
        </div>
    </div>
</template>
