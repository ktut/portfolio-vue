<script>

import Photoswipe from 'vue-pswipe';
import Vue from 'vue';

const options = {
            bgOpacity: 0.8,
            captionEl: false,
            tapToClose: true,
            shareEl: false,
            fullscreenEl: false,
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
    },
}

</script>

<template>
    <div>
        <Photoswipe class="photoswipe-gallery">
            <PhotoswipeItem class="photoswipe-image"
                v-for="(src, index) in photos"
                :key="index">
                <img
                    :data-src="src"
                    :data-pswp-src="src"
                    v-pswp="src"
                    class="lazy"
                />
            </PhotoswipeItem>
        </Photoswipe>
    </div>
</template>