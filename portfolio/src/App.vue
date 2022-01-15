<script>
// css
require('@/assets/styles/reset.css');
require('@/assets/styles/main.css');
require('@/assets/styles/transitions.css');
require('@/assets/styles/theme1.css');

// js
import Vue from 'vue';
import vueSmoothScroll from 'vue2-smooth-scroll';
import LazyLoad from "vanilla-lazyload";
import PhotoGrid from './components/PhotoGrid';
import photos from './data/photos';
import logos from './data/logos';
import printDesign from './data/printDesign';

Vue.use(vueSmoothScroll);

export default {
  name: 'app',
  components: {
    PhotoGrid
  },
  data() {
    return { 
      // is app loaded
      loaded: false,

      // image data to feed into galleries
      photos: photos,
      printDesign: printDesign,
      logos: logos,
      windowWidth: window.innerWidth,

      // section status
      sectionIntro: {
        show: false,
      },
      sectionChimag: {
        show: false,
      },
      sectionHb: {
        show: false,
      },
      sectionWebDesign: {
        show: true,
      },
      sectionPrintDesign: {
        show: false,
      },
      sectionCode: {
        show: false,
      },
      sectionPhoto: {
        show: true,
      },
      sectionUx: {
        show: false,
      },

      // stuff for header
      hueLeft: 0,
      hueRight: 0,
      // greeting: 'Hey there,',
      mouseXFocusScale: 1,
      // mouseYFocusPercentage: 50,
      selectedCategory: '',
      titleBackgroundURL: 'https://ktut.github.io/portfolio/assets/black-placeholder.jpg',
      videoBackgroundURL: '',
      showVideoBackground: false,

      themes: ['theme1'],
    }
  },
  mounted() {
    // this.updateGreetingByTimeOfDay();
    this.computeGradientHues();
    
    const lazyLoadInstance = new LazyLoad({
        elements_selector: ".lazy"
    });
    lazyLoadInstance.update();

    this.loaded = true
  },
  computed: {
    isTouchDevice() {
      if ("ontouchstart" in document.documentElement) {
        return true;
      } else {
        return false;
      }
    },
    colorCard() {
      return `
      background-color: hsla(${this.hueRight}, 100%, 50%,0.6);`;
    },
    colorCardLeft() {
      return `
      transform: scaleX(${this.mouseXFocusScale});
      background-color: hsla(${this.hueLeft}, 100%, 50%,0.6)`;
    },
    colorCardImage() {
      return 'background-image: url("' + this.titleBackgroundURL + '")';
    }
  },
  methods: {
    computeGradientHues() {
      this.hueLeft = parseInt(Math.random() * 270);
      this.hueRight = this.hueLeft / 2;
    },
    toggleSection(section) {
      if (this[section].show === true) {
        this[section].show = false;
      } else {
        this[section].show = true;
      }
    },
    getMousePosition() {
      let cursorX = event.pageX;
      let titleWidth = document.getElementById('title').offsetWidth;
      this.mouseXFocusScale = (cursorX / titleWidth).toFixed(3) * 2;

      // let cursorY = event.pageY;
      // let titleHeight = document.getElementById('title').offsetHeight;
      // this.mouseYFocusPercentage = parseInt((cursorY / titleHeight).toFixed(2) * 100);
    },
    // updateGreetingByTimeOfDay() {
    //   const currentTime = new Date().getHours();

    //   if (0 <= currentTime&&currentTime < 4) {
    //   // nighttime
    //    this.greeting = 'Welcome, night owl!';
    //   }
    //   if (5 <= currentTime&&currentTime < 10) {
    //   // morning
    //    this.greeting = 'Good morning!';
    //   }
    //   if (10 <= currentTime&&currentTime < 16) {
    //   // day
    //    this.greeting = 'Good day!';
    //   }
    //   if (16 <= currentTime&&currentTime < 18) {
    //     // evening
    //    this.greeting = 'Good afternoon!';
    //   }
    //   if (18 <= currentTime&&currentTime <= 24) {
    //     // nighttime
    //    this.greeting = 'Good evening!';
    //   }
    // }
  }
}

</script>

<template>
  <div id="app">
  
  <!-- <div class="title-contain" :style="colorCardImage">

    <transition name="fade">
      <video class="title-video" autoplay loop muted playsinline v-if="showVideoBackground" poster="https://ktut.github.io/portfolio/assets/farmers-design4.jpg">
        <source :src="videoBackgroundURL">
        Your browser does not support the video tag.
      </video>
    </transition>
    
    <section class="title" id="title" :style="colorCardGradient" @mousemove="updateGradientPosition()">
      <h2>{{greeting}}</h2>
      <h1>I’m Ramzi Dreessen.</h1>

      <h2>
        I’m a <a href="#web-design" v-on:click="sectionWebDesign.show = true" v-smooth-scroll @mouseover="showVideoBackground = true, titleBackgroundURL = '', videoBackgroundURL = 'https://ktut.github.io/portfolio/assets/farmers-design4.mov'">web designer</a>/<wbr><a href="#code" v-on:click="sectionCode.show = true" v-smooth-scroll @mouseover="showVideoBackground = true, titleBackgroundURL = '', videoBackgroundURL = 'https://ktut.github.io/portfolio/assets/farmers-design4.mov'">developer</a>, 

        <br><a href="#photo" v-smooth-scroll @mouseover="showVideoBackground = false, titleBackgroundURL = 'https://ktut.github.io/portfolio/assets/william.jpg'">photographer</a>, 

        <br><a href="http://www.rkdvisuals.com/video" target="_blank" rel="noreferrer noopener" @mouseover="showVideoBackground = true, titleBackgroundURL = '', videoBackgroundURL = 'https://ktut.github.io/portfolio/assets/rendered/vid-comp1.mp4'">videographer</a>, 

        <br><a href="#print-design" v-smooth-scroll @mouseover="showVideoBackground = false, titleBackgroundURL = 'https://ktut.github.io/portfolio/assets/cst-cover.jpg'">print designer</a>,

        <br>and more.
       </h2>
    </section>

  </div> -->

  <section class="newtitle webkitForceHardwareAcceleration" id="title" v-bind:class="{ loaded: loaded }">

    <!-- <div class="colors" v-bind:style="colorCard">
      <div class="left" v-bind:style="colorCardLeft"></div>
      <div class="right"></div>
    </div> -->

    <div class="logo" v-bind:class="[selectedCategory]">
      <div class="letter r webkitForceHardwareAcceleration">
        <div class="top webkitForceHardwareAcceleration"></div>
        <div class="bottom webkitForceHardwareAcceleration"></div>
      </div>
      <div class="letter k webkitForceHardwareAcceleration">
        <div class="top webkitForceHardwareAcceleration"></div>
        <div class="bottom webkitForceHardwareAcceleration"></div>
      </div>
      <div class="letter d webkitForceHardwareAcceleration">
        <div class="top webkitForceHardwareAcceleration"></div>
        <div class="bottom webkitForceHardwareAcceleration"></div>
      </div>
    </div>
    
    <nav @mouseleave="selectedCategory = ''"  v-bind:class="[selectedCategory]" class="webkitForceHardwareAcceleration">
      <a class="punch" @mouseenter="getMousePosition(), selectedCategory = 'webDesign'" href="#web-design" v-on:click="sectionWebDesign.show = true" v-smooth-scroll @mouseover="showVideoBackground = true, titleBackgroundURL = '', videoBackgroundURL = 'https://ktut.github.io/portfolio/assets/farmers-design4.mov'">Web Design</a>
      
      <a class="punch" @mouseenter="getMousePosition(), selectedCategory = 'code'" href="#code" v-on:click="sectionCode.show = true" v-smooth-scroll @mouseover="showVideoBackground = true, titleBackgroundURL = '', videoBackgroundURL = 'https://ktut.github.io/portfolio/assets/farmers-design4.mov'">Web Development</a> 

      <a @mouseenter="getMousePosition(), selectedCategory = 'printDesign'" href="#print-design" v-smooth-scroll @mouseover="showVideoBackground = false, titleBackgroundURL = 'https://ktut.github.io/portfolio/assets/cst-cover.jpg'">Print Design</a>

      <a @mouseenter="getMousePosition(), selectedCategory = 'photo'" href="#photo" target="_blank" rel="noreferrer noopener" v-smooth-scroll @mouseover="showVideoBackground = false, titleBackgroundURL = 'https://ktut.github.io/portfolio/assets/william.jpg'">Photo</a>

      <a @mouseenter="getMousePosition(), selectedCategory = 'video'" href="http://www.rkdvisuals.com/video" target="_blank" rel="noreferrer noopener" @mouseover="showVideoBackground = true, titleBackgroundURL = '', videoBackgroundURL = 'https://ktut.github.io/portfolio/assets/rendered/vid-comp1.mp4'">Video</a>
    </nav>
    
    <!-- <div class="image-contain" :style="colorCardImage">
      <transition name="fade">
        <video class="image-video" autoplay loop muted playsinline v-if="showVideoBackground" poster="https://ktut.github.io/portfolio/assets/farmers-design4.jpg">
          <source :src="videoBackgroundURL">
          Your browser does not support the video tag.
        </video>
      </transition>
    </div> -->
    
  </section>

  <section class="about smaller" id="about">
      <h2 style="color: black;">A little about me first.</h2>
      <img src="./assets/me.jpg" alt="Ramzi Dreessen" class="float">
      <p>Hi! I’m <b>Ramzi Dreessen</b>.</p>
      <p>I’ve never aligned myself to a particular job title. I enjoy planning, creating, reviewing, tearing apart my own work, rebuilding, finally shipping... any and all parts of the creative process.</p>
      <p>As a creator, I keep things simple. Good art, proper use of negative space, relevant typography, and staying in-tune with the “why” of the project. I’m aware that design without direction is just an aesthetics contest. With web design, I specialize in performative solutions that are fully responsive and utilize progressive enhancement.</p>

      <button class="readmore" v-on:click="toggleSection('sectionIntro')">
      {{ sectionIntro.show ? 'See Less -' : 'See More +' }}
      </button>

      <transition name="slide-fade">
        <div v-if="sectionIntro.show">
          <p>I understand component-based design, but I don’t believe in keeping design elements “sacred” across projects - to me, that’s just laziness. If you want someone to build you a cookie-cutter website filled with buzzwords and stock images (like one of these <a href="http://tiffzhang.com/startup" target="_blank" rel="noreferrer noopener">fake startup websites</a>), I’m probably not your guy. I value a strong art team and strong content, and working with others.</p>
          <p>I’m not afraid of complexity, but I also have a guideline: If I can't fully explain how something works to a non-technical person, in a concise manner, I find myself wondering why it was necessary to include in the first place.</p>
        </div>
      </transition>
  </section>

  <section class="brand-logos fullbleed">

    <p>Here are a few companies I’ve worked for, or worked with on a freelance basis:</p>
    <div class="outer-logo-slider">
      <div class="inner-logo-slider">
        <div class="brandlogo"
            v-for="(logo, index) in logos"
            v-bind:key="index">
            <img
                v-bind:src="logo.src"
                v-bind:style="logo.height"
            />
            <div class="tooltip">
              <span class="tooltip-inner">
                {{logo.tooltip}}
              </span>
            </div>
        </div>
      </div>
    </div>

  </section>

  <section class="web-design" id="web-design">
    <h2>I like building websites that people poke and prod on their tiny screens.</h2>
    <p>Currently I work for High 5 Games in New York City as a web developer (primarily doing programmatic design using React + Hooks). Previously, I was a junior software engineer at Fitch Ratings (using Vue.js, GraphQL and Atomic CSS), and before that, I was the web guy for <a href="http://www.chicagomag.com" target="_blank" rel="noreferrer noopener"><em>Chicago</em> magazine</a>, and attended Northwestern University’s full-stack coding bootcamp on nights/weekends. Here’s my <a href="https://github.com/ktut" target="_blank" rel="noreferrer noopener">Github</a>.</p> 
    <p style="margin-bottom: 10px;">At <em>Chicago</em>, I was in charge of web design and administration (taking over from the very talented <a href="https://www.seemann.com/luke/" target="_blank" rel="noreferrer noopener">Luke Seemann</a>), and <a href="https://citymag.org/crma_events/national-city-and-regional-magazine-2018-award-winners/" target="_blank" rel="noreferrer noopener">won a national award for online excellence</a> with my team from the City and Regional Magazine Association.</p>

    <!-- <button class="readmore" v-on:click="toggleSection('sectionWebDesign')">
      {{ sectionWebDesign.show ? 'See Less -' : 'See More +' }}
    </button> -->

    <transition name="slide-fade">
      <div v-if="sectionWebDesign.show">

        <p>Here’s some of the work I did there:</p>
      
        <ul class="resp">
          <li>
            <a class="no-resp web-img" href="http://web.archive.org/web/20180705121959/https://www.chicagomag.com/city-life/February-2018/A-Second-City-West-Side-Health-Life-Expectancy/" target="_blank" rel="noreferrer noopener">
              <video class="video lazy" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-1.mov">
                <source type="video/mp4" src="https://ktut.github.io/portfolio/assets/rendered/vid-1.mov">
                Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://web.archive.org/web/20180705121959/https://www.chicagomag.com/city-life/February-2018/A-Second-City-West-Side-Health-Life-Expectancy/" class="thumb" target="_blank" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-1.jpg');"></a>
            
            <div class="text">
              <a href="http://web.archive.org/web/20180705121959/https://www.chicagomag.com/city-life/February-2018/A-Second-City-West-Side-Health-Life-Expectancy/" target="_blank" rel="noreferrer noopener">A Second City</a> (design direction, interactive components, <a href="https://citymag.org/crma_events/2019-national-city-and-regional-magazine-awards-finalists/" target="_blank" rel="noreferrer noopener">2019 CRMA Finalist for Multiplatform Storytelling</a>)
            </div>
          </li>

          <li>
            <a class="no-resp web-img" href="http://web.archive.org/web/20180202212548/http://www.chicagomag.com/Chicago-Magazine/June-2017/Welcome-to-Refugee-High/" target="_blank" rel="noreferrer noopener">
              <video class="video lazy" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-2.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-2.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://web.archive.org/web/20180202212548/http://www.chicagomag.com/Chicago-Magazine/June-2017/Welcome-to-Refugee-High/" class="thumb" target="_blank" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-2.jpg');"></a>
            
            <div class="text">
              <a href="http://web.archive.org/web/20180202212548/http://www.chicagomag.com/Chicago-Magazine/June-2017/Welcome-to-Refugee-High/" target="_blank" rel="noreferrer noopener">Welcome to Refugee High</a> (video and interactive components, <a href="https://citymag.org/crma_events/2018-national-city-and-regional-magazine-awards-finalists/" target="_blank" rel="noreferrer noopener">2018 CRMA Finalist for Multiplatform Storytelling</a>)
            </div>
          </li>

          <li>
            <a class="no-resp web-img" href="https://web.archive.org/web/20201124144409/https://www.chicagomag.com/Chicago-Magazine/July-2017/Whats-In-Their-Fridge/" target="_blank" rel="noreferrer noopener">
              <video class="video lazy" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-3.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-3.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>

            <a href="https://web.archive.org/web/20201124144409/https://www.chicagomag.com/Chicago-Magazine/July-2017/Whats-In-Their-Fridge/" class="thumb" target="_blank" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-3.jpg');"></a>
            
            <div class="text">
              <a href="https://web.archive.org/web/20201124144409/https://www.chicagomag.com/Chicago-Magazine/July-2017/Whats-In-Their-Fridge/" target="_blank" rel="noreferrer noopener">What’s in Their Fridge</a> (3D transforms, SVGs, pseudo elements)
            </div>
          </li>

          <li>
            <a class="no-resp web-img" href="http://web.archive.org/web/20181004061833/http://www.chicagomag.com/Chicago-Magazine/June-2017/Farmers-Markets/" target="_blank" rel="noreferrer noopener">
              <video class="video lazy" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-6.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-6.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://web.archive.org/web/20181004061833/http://www.chicagomag.com/Chicago-Magazine/June-2017/Farmers-Markets/" class="thumb" target="_blank" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-6.jpg');"></a>
            
            <div class="text">
              <a href="http://web.archive.org/web/20181004061833/http://www.chicagomag.com/Chicago-Magazine/June-2017/Farmers-Markets/" target="_blank" rel="noreferrer noopener">A Guide to Farmer’s Markets</a> (photo deconstructed into flexbox components)
            </div>
          </li>

          <li>
            <a class="no-resp web-img" href="http://web.archive.org/web/20170719233806/https://www.chicagomag.com/Chicago-Magazine/May-2017/Faces-of-a-Century/" target="_blank" rel="noreferrer noopener">
              <video class="video lazy" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-5.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-5.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://web.archive.org/web/20170719233806/https://www.chicagomag.com/Chicago-Magazine/May-2017/Faces-of-a-Century/" class="thumb" target="_blank" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-5.jpg');"></a>
            
            <div class="text">
              <a href="http://web.archive.org/web/20170719233806/https://www.chicagomag.com/Chicago-Magazine/May-2017/Faces-of-a-Century/" target="_blank" rel="noreferrer noopener">Face of a Century</a> (custom gallery with audio integration)
            </div>
          </li>

          <li class="better-on-mobile">
            <a class="no-resp web-img" href="http://www.chicagomag.com/Chicago-Magazine/July-2017/Summer-Guide/Get-Beached/" target="_blank" rel="noreferrer noopener">
              <video class="video lazy" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-8.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-8.mov" type="video/mp4">
              Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://www.chicagomag.com/Chicago-Magazine/July-2017/Summer-Guide/Get-Beached/" class="thumb" target="_blank" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-8.jpg');"></a>
            
            <div class="text">
              <a href="http://www.chicagomag.com/Chicago-Magazine/July-2017/Summer-Guide/Get-Beached/" target="_blank" rel="noreferrer noopener">A Foolproof Guide to Finding the Best Beach for You</a> (interactive quiz)
            </div>
          </li>

          <li v-if="sectionChimag.show" class="better-on-mobile">
            <a class="no-resp web-img" href="http://www.chicagomag.com/Chicago-Magazine/November-2018/12-Blocks/" target="_blank" rel="noreferrer noopener">
              <video class="video lazy" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-10.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-10.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://www.chicagomag.com/Chicago-Magazine/November-2018/12-Blocks/" class="thumb" target="_blank" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-10.jpg');"></a>
            
            <div class="text">
              <a href="http://www.chicagomag.com/Chicago-Magazine/November-2018/12-Blocks/" target="_blank" rel="noreferrer noopener">Twelve Blocks</a> (responsive design and interactivity)
            </div>
          </li>

          <li v-if="sectionChimag.show" class="better-on-mobile">
              <a class="no-resp web-img" href="http://web.archive.org/web/20180320110712/https://www.chicagomag.com/Chicago-Magazine/March-2018/Spring-Fashion-2018/" target="_blank" rel="noreferrer noopener">
                <video class="video lazy" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-4.mov">
                  <source src="https://ktut.github.io/portfolio/assets/rendered/vid-4.mov" type="video/mp4">
                Your browser does not support the video tag.
                </video>
            </a>

            <a href="http://web.archive.org/web/20180320110712/https://www.chicagomag.com/Chicago-Magazine/March-2018/Spring-Fashion-2018/" class="thumb" target="_blank" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-4.jpg');"></a>
            
            <div class="text">
              <a href="http://web.archive.org/web/20180320110712/https://www.chicagomag.com/Chicago-Magazine/March-2018/Spring-Fashion-2018/" target="_blank" rel="noreferrer noopener">Spring Fashion: Pattern Recognition</a> (SVG masking, lazyloading, custom scrolling)
            </div>
          </li>

          <li v-if="sectionChimag.show" class="better-on-mobile">
            <a class="no-resp web-img" href="http://web.archive.org/web/20180106051955/https://www.chicagomag.com/chicago-magazine/january-2018/top-doctors/" target="_blank" rel="noreferrer noopener">
              <video class="video lazy" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-11.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-11.mov" type="video/mp4">
              Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://web.archive.org/web/20180106051955/https://www.chicagomag.com/chicago-magazine/january-2018/top-doctors/" class="thumb" target="_blank" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-11.jpg');"></a>
            
            <div class="text">
              <a href="http://web.archive.org/web/20180106051955/https://www.chicagomag.com/chicago-magazine/january-2018/top-doctors/" target="_blank" rel="noreferrer noopener">Top Doctors</a> (animation, responsive design)
            </div>
          </li>

          <li v-if="sectionChimag.show">
            <a class="no-resp web-img" href="http://www.chicagomag.com/Chicago-Magazine/August-2018/What-Trauma-Docs-Know/" target="_blank" rel="noreferrer noopener">
              <video class="video lazy" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-9.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-9.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://www.chicagomag.com/Chicago-Magazine/August-2018/What-Trauma-Docs-Know/" class="thumb" target="_blank" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-9.jpg');"></a>
            
            <div class="text">
              <a href="http://www.chicagomag.com/Chicago-Magazine/August-2018/What-Trauma-Docs-Know/" target="_blank" rel="noreferrer noopener">What Trauma Docs Know</a> (CSS Grid, typography)
            </div>
          </li>

          <li v-if="sectionChimag.show">
            <a class="no-resp web-img" href="http://www.chicagomag.com/Chicago-Magazine/August-2018/House-Music/" target="_blank" rel="noreferrer noopener">
              <video class="video lazy" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-12.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-12.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://www.chicagomag.com/Chicago-Magazine/August-2018/House-Music/" class="thumb" target="_blank" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-12.jpg');"></a>
            
            <div class="text">
              <a href="http://www.chicagomag.com/Chicago-Magazine/August-2018/House-Music/" target="_blank" rel="noreferrer noopener">Chicago House Music</a> (Spotify integration, interactive Roland TB-303)
            </div>
          </li>

          <li v-if="sectionChimag.show">
            <a class="no-resp web-img" href="http://web.archive.org/web/20171123234228/https://www.chicagomag.com/chicago-magazine/september-2017/how-to-buy-art/" target="_blank" rel="noreferrer noopener">
              <video class="video lazy" width="100%" autoplay loop muted playsinline poster="https://ktut.github.io/portfolio/assets/rendered/vid-7-poster.jpg" src="https://ktut.github.io/portfolio/assets/rendered/vid-7.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-7.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>
            <a href="http://web.archive.org/web/20171123234228/https://www.chicagomag.com/chicago-magazine/september-2017/how-to-buy-art/" class="thumb" target="_blank" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-7.jpg');"></a>
            
            <div class="text">
              <a href="http://web.archive.org/web/20171123234228/https://www.chicagomag.com/chicago-magazine/september-2017/how-to-buy-art/" target="_blank" rel="noreferrer noopener">How to Buy Art</a> (responsive design using viewheight units)
            </div>
          </li>


          <li v-if="sectionChimag.show">
            <a class="no-resp web-img" href="https://www.chicagomag.com/Chicago-Magazine/June-2017/Whos-Got-Next/" target="_blank" rel="noreferrer noopener">
              <video class="video lazy" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-13.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-13.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>
            <a href="https://www.chicagomag.com/Chicago-Magazine/June-2017/Whos-Got-Next/" class="thumb" target="_blank" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-13.jpg');"></a>
            
            <div class="text">
              <a href="https://www.chicagomag.com/Chicago-Magazine/June-2017/Whos-Got-Next/" target="_blank" rel="noreferrer noopener">Who’s Got Next</a> (responsive design and transforms)
            </div>
          </li>


          <li v-if="sectionChimag.show">
            <a class="no-resp web-img" href="https://www.chicagomag.com/Chicago-Magazine/July-2017/Summer-Guide/Eat-It-on-a-Stick/" target="_blank" rel="noreferrer noopener">
              <video class="video lazy" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-14.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-14.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>
            <a href="https://www.chicagomag.com/Chicago-Magazine/July-2017/Summer-Guide/Eat-It-on-a-Stick/" class="thumb" target="_blank" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-14.jpg');"></a>
            
            <div class="text">
              <a href="https://www.chicagomag.com/Chicago-Magazine/July-2017/Summer-Guide/Eat-It-on-a-Stick/" target="_blank" rel="noreferrer noopener">Eat It on a Stick</a> (hover effects and design)
            </div>
          </li>


          <li v-if="sectionChimag.show">
            <a class="no-resp web-img" href="https://www.chicagomag.com/Chicago-Magazine/December-2017/Chicagoans-of-the-Year/" target="_blank" rel="noreferrer noopener">
              <video class="video lazy" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-15.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-15.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>
            <a href="https://www.chicagomag.com/Chicago-Magazine/December-2017/Chicagoans-of-the-Year/" class="thumb" target="_blank" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-15.jpg');"></a>
            
            <div class="text">
              <a href="https://www.chicagomag.com/Chicago-Magazine/December-2017/Chicagoans-of-the-Year/" target="_blank" rel="noreferrer noopener">Chicagoans of the Year</a> (custom SVGs and event integration)
            </div>
          </li>

          <button class="readmore" v-on:click="toggleSection('sectionChimag')">{{ sectionChimag.show ? 'See Less -' : 'See More +' }}</button>
        </ul>

      </div>
    </transition>
    
  </section>

     <!-- v-bind:class="[selectedCategory]" -->
  <section class="hb" style="max-width: 900px; margin: 0 auto;" id="code">
    <video v-bind:class="`video lazy hb-mobile small first ${[sectionHb.show]}`"  width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/HB-mobile-2.mp4"></video>
    <h2>I enjoy being the utility guy.</h2>
    <p>I’m no stranger to acting as a one-man agency for the right project. For Chicago-based real estate company Hudson Burnham, they wanted a homepage that would attract attention and play nicely with their slogan "Move Up". They wanted a video background unlike any of their competitors - stock footage wouldn't cut it.</p> 


    <transition name="slide-fade">
      <div v-if="sectionHb.show">
        <p class="overview">
          <img src="https://ktut.github.io/portfolio/assets/city-drawing-2.png" class="city"/>
          <img src="https://ktut.github.io/portfolio/assets/camera-angle.png" class="camera"/>
        </p>

        <p>I knew we’d need a couple tall buildings in the front of the shot, to work with the theme, with the Sears Tower (as true Chicagoans call it) anchoring the background. I assumed we'd shoot in the golden hour for optimal lighting.</p>

        <p>The drone pilot was able to shoot from about 3,000 feet up and rotate downward in a helix motion, stabilized by the Mavic 2’s Hyperlapse feature (essentially, shooting automatically-comp’d stills instead of video). After reversing, speed-ramping and color-grading the footage in Premiere, I was ready to start coding.</p>

        <p>I created a custom template for the Wordpress site I was building, and ensured that we were handling the different crop positions and optimal file formats for each platform:</p>

        <!-- <p>
          <img src="https://ktut.github.io/portfolio/assets/hb-code.png" style="width: 100%;">
        </p> -->
        <p style="max-width: 635px; max-height: 200px; overflow-y: auto; border: 1px solid #bbb; clear:both;">
          <!-- <img src="https://ktut.github.io/portfolio/assets/hb-code.png" style="width: 100%; vertical-align: middle;"> -->
          <picture>
            <source 
            style="width: 100%; vertical-align: middle;"
              srcset="https://ktut.github.io/portfolio/assets/hb-code.png"
              media="(min-width: 600px)"
            />
            <img 
            style="width: 100%; vertical-align: middle;"
              src="https://ktut.github.io/portfolio/assets/hb-code-mobile.png" 
            />
          </picture>
        </p>

        <p>The final result is not only performant (loads within 1-2 seconds, streaming the video as it plays), but it looks great as well:</p>
        <!-- v-if="windowWidth <= 400"  -->
        <p style="position: relative; max-width: 900px;">
          <video class="`video lazy hb-mobile large"  width="100%" autoplay loop muted playsinline controls src="https://ktut.github.io/portfolio/assets/rendered/HB-mobile-2.mp4"></video>
          <video v-if="windowWidth > 400" class="video lazy hb-desktop" width="100%" autoplay loop muted playsinline controls src="https://ktut.github.io/portfolio/assets/rendered/HB-desktop-2.mp4"></video>
        </p>

      </div>
    </transition>

    <button class="readmore" v-on:click="toggleSection('sectionHb')" style="clear:both;">{{ sectionHb.show ? 'See Less -' : 'See More +' }}</button>


  </section>

  <section class="code">

    <h2>I enjoy exploring new intersections of programming and design.<span v-if="!sectionCode.show">..</span></h2>

    <p>At Fitch Ratings, I worked with with component-based design and architecture, and was interested in how we could better use patterning and rulesets to improve both the user and developer experiences.</p>

    <button class="readmore" v-on:click="toggleSection('sectionCode')">{{ sectionCode.show ? 'See Less -' : 'See More +' }}</button>

    <transition name="slide-fade">
        <div v-if="sectionCode.show">

        <p>We needed a way to induce visual variety (without a lot of extra developer effort), on pages that had card components with anywhere from one to twenty articles in them.</p>
        <p>In the solution I devised, the developer building the page simply feeds a "card" component an array of article objects, and the component designs itself, using a simple patterning ruleset that plucks atomic classes from an array. Fun stuff:</p>

        <p>
          <video class="video lazy" width="100%" autoplay loop muted playsinline controls src="https://ktut.github.io/portfolio/assets/rendered/fitch-1.mov">
            <source src="https://ktut.github.io/portfolio/assets/rendered/fitch-1.mov" type="video/mp4">
            Your browser does not support the video tag.
          </video>
        </p>

        <p>Here's what happens when you add this a bunch of cards, all held together with some CSS Grid:</p>

        <p style="max-width: 900px;">
          <video class="video lazy" width="100%" autoplay loop muted playsinline controls src="https://ktut.github.io/portfolio/assets/rendered/fitch-2.mov">
            <source src="https://ktut.github.io/portfolio/assets/rendered/fitch-2.mov" type="video/mp4">
            Your browser does not support the video tag.
          </video>
        </p>
        </div>
    </transition>

  </section>
  
  <section class="ux" id="ux">

    <h2><span v-if="!sectionUx.show">... as well as</span><span v-if="sectionUx.show">I enjoy exploring</span> intersections of UI and UX.</h2>

    <p>My user experience philosophy is centered around streamlining common pathways, <a href="https://www.nngroup.com/articles/minimize-cognitive-load/" target="_blank" rel="noreferrer noopener">reducing cognitive load</a> and improving design (duh).</p>

    <button class="readmore" v-on:click="toggleSection('sectionUx')">{{ sectionUx.show ? 'See Less -' : 'See More +' }}</button>

    <transition name="slide-fade">
      <div v-if="sectionUx.show">
    
      <p>At <em>Chicago</em>, I was tasked with overhauling our subscription page. The old page had few conversions per user, and it was clear as to why:</p>

      <p>
        <img src="https://ktut.github.io/portfolio/assets/purchase-old.jpg" style="width: 100%;">
      </p>

      <p>The most important, relevant and well-produced visuals (the covers) were the smallest elements on the page, while the largest page element (the copy) wasn't even relevant to the page's primary purpose (to convert visitors into paid subscribers of the print product). Hiding the most important fields within tabs prevented the user from easily accessing them, and it wasn't even clear what order the tabs were meant to be clicked. Even our own staff was confused about how to use the interface.</p>

      <p>I studied the in-page analytics, researched current industry best practices, and talked with a few of my friends (including <a href="http://bruceackerman.com/" target="_blank" rel="noreferrer noopener">Bruce Ackerman</a>, former head of UX at <a href="https://www.avant.com/" target="_blank" rel="noreferrer noopener">Avant</a>). I settled on a simpler approach:</p>

      <p style="max-width: 900px; max-height: 675px; overflow-y: auto; border: 1px solid #bbb;">
        <img src="https://ktut.github.io/portfolio/assets/purchase-new-lg-2.jpg" style="width: 100%; vertical-align: middle;">
        <!-- <iframe src="http://web.archive.org/web/20180121131738/https://cma.pcdfusion.com/pcd/Order?iKey=I**D7B" style="width: 100%; min-height: 600px; border: 1px solid #bbb;"></iframe> -->
      </p>

      <p>I put the call to action and purchaseable products front and center, and ensured that no important information was hidden from the user.</p>
      <p>After the design of the page was completed, I worked directly with our vendor to eliminate unnecessary fields, handle security checks, and create a more direct experience between the load of the page and the click of the "Purchase" button.</p>
      <p>In the six months following the implementation of the new design, conversions per visitor went up 20%.</p>

      </div>
    </transition>

  </section>

  <section class="print-design fullbleed" id="print-design">
    <br>
    <hr>
    <br>
    <h2>Did the whole CMYK thing, too.</h2>

    <p>My interest in web design stemmed from print design, starting at the Chicago Sun-Times in 2012 and culminating at <em>Chicago</em> in 2016. Two of the biggest projects I worked on there were:</p>
    <p><b>1.</b> Designing a 103-page glossy embossed hardcover book for the Chicago Sun-Times Foundation in Fall/Winter 2015, including hundreds of photos that I shot over four years of covering the biggest philanthropic events in the city.</p>
    <p><b>2.</b> As a part of a three-person team, designed a 24-page glossy lifestyle magazine (SPLASH) from 2012-2016. Circulation: 225,000.</p>

    <!-- <button class="readmore" v-on:click="toggleSection('sectionPrintDesign')">
      {{ sectionPrintDesign.show ? 'Make Smaller -' : 'Make Bigger +' }}
    </button> -->

    <PhotoGrid v-bind:photos="printDesign" v-bind:template="'wide-gallery'"></PhotoGrid>

  </section>

  <section class="photo fullbleed" id="photo">

    <br>

    <h2>Sometimes I take photos.</h2>

    <p>I've been shooting for eight years now, both on my own and on staff at Chicago Sun-Times SPLASH and <em>Chicago</em>. Check out more on my dedicated <a href="http://www.rkdvisuals.com" target="_blank" rel="noreferrer noopener">photo portfolio site</a>.</p>

    <!-- <button class="readmore hide-on-mobile" v-on:click="toggleSection('sectionPhoto')">{{ sectionPhoto.show ? 'See Less -' : 'See More +' }}</button> -->
    <transition name="slide-fade">
      <div v-if="sectionPhoto.show">
        <PhotoGrid v-bind:photos="photos"></PhotoGrid>
      </div>
    </transition>

  </section>


  <section class="contact" id="contact">

    <br>

    <h2>Let’s chat!</h2>

    <p>You can reach me by email at <a href="mailto:ramzidreessen@gmail.com?Subject=Saw%20your%20site%20at%20rkdvis.com" target="_top">ramzidreessen@gmail.com</a>. Please put relevant information in the subject line. If we've already worked together, please feel free to add me as a contact on <a href="https://www.linkedin.com/in/ramzidreessen/" target="_blank" rel="noreferrer noopener">LinkedIn</a>.</p>
    <br>
    <p class="small">Video and images copyright Ramzi Dreessen 2008 - 2019. Photo and video content is protected by U.S. Copyright Law and is NOT Public Domain, and may not be manipulated, copied, published, reproduced, downloaded, or used in any manner without prior consent of Ramzi Dreessen. Select web design and photo content is copyrighted by SPLASH PUBLICATIONS, LLC, Tribune Publishing or Fitch Ratings and may not be manipulated, copied, published, reproduced, downloaded, or used in any manner without prior consent of SPLASH PUBLICATIONS, LLC, Tribune Publishing or Fitch Ratings.</p>
  </section>
  
  </div>
</template>
