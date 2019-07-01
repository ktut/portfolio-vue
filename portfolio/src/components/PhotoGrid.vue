<script>

import Photoswipe from 'vue-pswipe';
import Vue from 'vue';

const options = {
            bgOpacity: 0.8,
            captionEl: false,
            tapToClose: true,
            shareEl: false,
            fullscreenEl: false,
            preload: [0,1],
        };

Vue.use(Photoswipe, options);

export default {
    name: 'PhotoGrid',
    props: {
        photos: {
            type: Array,
            required: true,
            default: () => [],
        },
        template: {
            type: String,
            required: false,
            default: 'photoswipe-gallery',
        },
    },
}

</script>

<template>
    <div>
        <Photoswipe v-bind:class="template">
            <div class="photoswipe-image"
                v-for="(src, index) in photos"
                :key="index">
                <img
                    :data-src="src"
                    :data-pswp-src="src"
                    v-pswp="src"
                    class="lazy"
                />
            </div>
        </Photoswipe>
    </div>
</template>