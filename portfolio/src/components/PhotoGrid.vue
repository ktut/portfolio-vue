<script>

// import Photoswipe from 'vue-pswipe';
// import Vue from 'vue';

// const options = {
//             bgOpacity: 0.8,
//             captionEl: false,
//             tapToClose: true,
//             shareEl: false,
//             fullscreenEl: false,
//         };

// Vue.use(Photoswipe, options);

export default {
    name: 'PhotoGrid',
    data() {
        return {
            photos: [
                '/photos/ruffalo-1.jpg',
                '/photos/WhoWatchR-SLH-122114.01-2.JPG',
                '/photos/will-1100.jpg',
                '/photos/IMG_0038-2.jpg',
                '/photos/IMG_0905.jpg',
                '/photos/1100-westwick.jpg',
                '/photos/00-aless.jpg',
                '/photos/miles-49-RAMZI-DREESSEN.jpg',
                '/photos/PhotoJ-RKD-1.jpg',
                '/photos/10572022_3409851362463_3147035676682537141_o.jpg',
                '/photos/E8A2046-WEB.jpg',
                '/photos/IMG-365.jpg',
                '/photos/lefty-3.jpg',
            ],
        }
    },
}

</script>

<template>
    <div>
        <div class="photoswipe-gallery">
            <div class="photoswipe-image"
                v-for="(src, index) in photos"
                :key="index">
                <img
                    :data-src="src"
                    :data-pswp-src="src"
                    class="lazy"
                />
            </div>
        </div>
    </div>
</template>