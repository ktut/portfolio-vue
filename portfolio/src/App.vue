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

Vue.use(vueSmoothScroll);

export default {
  name: 'app',
  data() {
    return { 
      sectionWebDesign: {
        show: false,
        message: "Expand Section +",
      },
      sectionCode: {
        show: false,
        message: "Expand Section +",
      },
      sectionUx: {
        show: false,
        message: "Expand Section +",
      },
      greeting: 'Hey there,',
      themes: ['theme1'],
      gradientFocusPercentage: 0,
      // default background image
      titleBackgroundURL: 'https://ktut.github.io/portfolio/assets/black-placeholder.jpg',
      videoBackgroundURL: '',
      showVideoBackground: false,
    }
  },
  mounted() {
    this.updateGreetingByTimeOfDay();
    const lazyLoadInstance = new LazyLoad({
        elements_selector: ".lazy"
    });
    lazyLoadInstance.update();
  },
  computed: {
    titleCardGradient() {
      return 'background-image: linear-gradient(rgba(0,0,0,0.4) 0%, rgba(0,0,0,0.2) ' + this.gradientFocusPercentage + '%, rgba(238,238,238,1) 100%)';
    },
    titleCardImage() {
      return 'background-image: url("' + this.titleBackgroundURL + '")';
    }
  },
  methods: {
    toggleSection(section) {
      if (this[section].show === true) {
        this[section].show = false;
        this[section].message = "Expand Section +";
      } else {
        this[section].show = true;
        this[section].message = "Collapse Section -";
      }
    },
    updateGradientPosition() {
      let cursorY = event.pageY;
      let titleHeight = document.getElementById('title').offsetHeight;
      this.gradientFocusPercentage = parseInt((cursorY / titleHeight).toFixed(2) * 100);
    },
    updateGreetingByTimeOfDay() {
      const currentTime = new Date().getHours();

      if (0 <= currentTime&&currentTime < 4) {
      // nighttime
       this.greeting = 'Welcome, night owl!';
      }
      if (5 <= currentTime&&currentTime < 11) {
      // morning
       this.greeting = 'Good morning!';
      }
      if (11 <= currentTime&&currentTime < 16) {
      // day
       this.greeting = 'Good day!';
      }
      if (16 <= currentTime&&currentTime < 18) {
        // evening
       this.greeting = 'Good afternoon!';
      }
      if (18 <= currentTime&&currentTime <= 24) {
        // nighttime
       this.greeting = 'Good evening!';
      }
    }
  }
}

</script>

<template>
  <div id="app">
  
  <div class="title-contain" :style="titleCardImage">

    <transition name="fade">
      <video class="title-video" autoplay loop muted playsinline v-if="showVideoBackground" poster="https://ktut.github.io/portfolio/assets/farmers-design4.jpg">
        <source :src="videoBackgroundURL">
        Your browser does not support the video tag.
      </video>
    </transition>
    
    <section class="title" id="title" :style="titleCardGradient" @mousemove="updateGradientPosition()">
      <h2>{{greeting}}</h2>
      <h1>I’m Ramzi.</h1>

      <h2>
        I’m a <a id="test" href="#web-design"  v-on:click="sectionWebDesign.show = true" v-smooth-scroll @mouseover="showVideoBackground = true, titleBackgroundURL = '', videoBackgroundURL = 'https://ktut.github.io/portfolio/assets/farmers-design4.mov'">web designer and developer</a>, 

        <br><a href="http://www.rkdvisuals.com" target="_blank" @mouseover="showVideoBackground = false, titleBackgroundURL = 'https://ktut.github.io/portfolio/assets/william.jpg'">photographer</a>, 

        <br><a href="http://www.rkdvisuals.com/video" target="_blank" @mouseover="showVideoBackground = true, titleBackgroundURL = '', videoBackgroundURL = 'https://ktut.github.io/portfolio/assets/rendered/vid-comp1.mp4'">videographer</a>, 

        <br><a href="http://www.rkdvisuals.com/design/" target="_blank" @mouseover="showVideoBackground = false, titleBackgroundURL = 'https://ktut.github.io/portfolio/assets/cst-cover.jpg'">print designer</a>,

        <br>and more.
       </h2>
    </section>
  </div>

  <section class="about" id="about">
      <p>Currently I do front end web development for Fitch Ratings (using Vue.js, GraphQL, Node, Atomic CSS). Previously, I was the web guy for <a href="http://www.chicagomag.com" target="_blank"><em>Chicago</em></a> magazine, and attended Northwestern University’s full-stack coding bootcamp on nights/weekends (learning React, Mongo and MySQL). Here's my <a href="https://github.com/ktut" target="_blank">Github</a>.</p> 
  </section>

  <section class="web-design" id="web-design">
    <p style="margin-bottom: 10px;">At <em>Chicago</em>, I was in charge of web design, and <a href="https://citymag.org/crma_events/national-city-and-regional-magazine-2018-award-winners/" target="_blank">won a national award</a> from the City and Regional Magazine Association.</p>

    <button class="readmore" v-on:click="toggleSection('sectionWebDesign')">{{sectionWebDesign.message}}</button>

    <transition name="slide-fade">
      <div v-if="sectionWebDesign.show">

        <p>Here’s some of the work I did there:</p>
      
        <ul class="resp">
          <li>
            <a class="no-resp web-img" href="http://www.chicagomag.com/city-life/February-2018/A-Second-City-West-Side-Health-Life-Expectancy/" target="_blank">
              <video class="video" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-1.mov">
                <source type="video/mp4" src="https://ktut.github.io/portfolio/assets/rendered/vid-1.mov">
                Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://www.chicagomag.com/city-life/February-2018/A-Second-City-West-Side-Health-Life-Expectancy/" class="thumb" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-1.jpg');"></a>
            
            <div class="text">
              <a href="http://www.chicagomag.com/city-life/February-2018/A-Second-City-West-Side-Health-Life-Expectancy/" target="_blank">A Second City</a> (design direction, interactive components, <a href="https://citymag.org/crma_events/2019-national-city-and-regional-magazine-awards-finalists/" target="_blank">2019 CRMA Finalist for Multiplatform Storytelling</a>)
            </div>
          </li>

          <li>
            <a class="no-resp web-img" href="http://www.chicagomag.com/Chicago-Magazine/June-2017/Welcome-to-Refugee-High/" target="_blank">
              <video class="video" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-2.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-2.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://www.chicagomag.com/Chicago-Magazine/June-2017/Welcome-to-Refugee-High/" class="thumb" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-2.jpg');"></a>
            
            <div class="text">
              <a href="http://www.chicagomag.com/Chicago-Magazine/June-2017/Welcome-to-Refugee-High/" target="_blank">Welcome to Refugee High</a> (video/interactive components, <a href="https://citymag.org/crma_events/2018-national-city-and-regional-magazine-awards-finalists/" target="_blank">2018 CRMA Finalist for Multiplatform Storytelling</a>)
            </div>
          </li>

          <li>
            <a class="no-resp web-img" href="http://www.chicagomag.com/Chicago-Magazine/July-2017/Whats-In-Their-Fridge/" target="_blank">
              <video class="video" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-3.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-3.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://www.chicagomag.com/Chicago-Magazine/July-2017/Whats-In-Their-Fridge/" class="thumb" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-3.jpg');"></a>
            
            <div class="text">
              <a href="http://www.chicagomag.com/Chicago-Magazine/July-2017/Whats-In-Their-Fridge/" target="_blank">What’s in Their Fridge</a> (3D transforms, SVGs, pseudo elements)
            </div>
          </li>

          <li>
            <a class="no-resp web-img" href="http://www.chicagomag.com/Chicago-Magazine/May-2017/Faces-of-a-Century/" target="_blank">
              <video class="video" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-5.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-5.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://www.chicagomag.com/Chicago-Magazine/May-2017/Faces-of-a-Century/" class="thumb" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-5.jpg');"></a>
            
            <div class="text">
              <a href="http://www.chicagomag.com/Chicago-Magazine/May-2017/Faces-of-a-Century/" target="_blank">Face of a Century</a> (custom gallery with audio integration)
            </div>
          </li>

          <li>
            <a class="no-resp web-img" href="http://www.chicagomag.com/Chicago-Magazine/June-2017/Farmers-Markets/" target="_blank">
              <video class="video" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-6.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-6.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://www.chicagomag.com/Chicago-Magazine/June-2017/Farmers-Markets/" class="thumb" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-6.jpg');"></a>
            
            <div class="text">
              <a href="http://www.chicagomag.com/Chicago-Magazine/June-2017/Farmers-Markets/" target="_blank">A Guide to Farmer’s Markets</a> (photo deconstructed into flexbox components)
            </div>
          </li>

          <li>
              <a class="no-resp web-img" href="http://www.chicagomag.com/Chicago-Magazine/March-2018/Spring-Fashion-2018/" target="_blank">
                <video class="video" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-4.mov">
                  <source src="https://ktut.github.io/portfolio/assets/rendered/vid-4.mov" type="video/mp4">
                Your browser does not support the video tag.
                </video>
            </a>

            <a href="http://www.chicagomag.com/Chicago-Magazine/March-2018/Spring-Fashion-2018/" class="thumb" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-4.jpg');"></a>
            
            <div class="text">
              <a href="http://www.chicagomag.com/Chicago-Magazine/March-2018/Spring-Fashion-2018/" target="_blank">Spring Fashion: Pattern Recognition</a> (SVG masking, lazyloading, custom scrolling)
            </div>
          </li>

          <li>
            <a class="no-resp web-img" href="http://www.chicagomag.com/Chicago-Magazine/July-2017/Summer-Guide/Get-Beached/" target="_blank">
              <video class="video" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-8.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-8.mov" type="video/mp4">
              Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://www.chicagomag.com/Chicago-Magazine/July-2017/Summer-Guide/Get-Beached/" class="thumb" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-8.jpg');"></a>
            
            <div class="text">
              <a href="http://www.chicagomag.com/Chicago-Magazine/July-2017/Summer-Guide/Get-Beached/" target="_blank">A Foolproof Guide to Finding the Best Beach for You</a> (interactive quiz)
            </div>
          </li>

          <li>
            <a class="no-resp web-img" href="http://www.chicagomag.com/Chicago-Magazine/November-2018/12-Blocks/" target="_blank">
              <video class="video" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-10.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-10.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://www.chicagomag.com/Chicago-Magazine/November-2018/12-Blocks/" class="thumb" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-10.jpg');"></a>
            
            <div class="text">
              <a href="http://www.chicagomag.com/Chicago-Magazine/November-2018/12-Blocks/" target="_blank">Twelve Blocks</a> (responsive design and interactivity)
            </div>
          </li>

          <li>
            <a class="no-resp web-img" href="http://www.chicagomag.com/Chicago-Magazine/January-2018/Top-Doctors/" target="_blank">
              <video class="video" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-11.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-11.mov" type="video/mp4">
              Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://www.chicagomag.com/Chicago-Magazine/January-2018/Top-Doctors/" class="thumb" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-11.jpg');"></a>
            
            <div class="text">
              <a href="http://www.chicagomag.com/Chicago-Magazine/January-2018/Top-Doctors/" target="_blank">Top Doctors</a> (animation, responsive design)
            </div>
          </li>

          <li>
            <a class="no-resp web-img" href="http://www.chicagomag.com/Chicago-Magazine/August-2018/What-Trauma-Docs-Know/" target="_blank">
              <video class="video" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-9.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-9.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://www.chicagomag.com/Chicago-Magazine/August-2018/What-Trauma-Docs-Know/" class="thumb" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-9.jpg');"></a>
            
            <div class="text">
              <a href="http://www.chicagomag.com/Chicago-Magazine/August-2018/What-Trauma-Docs-Know/" target="_blank">What Trauma Docs Know</a> (CSS Grid, typography)
            </div>
          </li>

          <li>
            <a class="no-resp web-img" href="http://www.chicagomag.com/Chicago-Magazine/August-2018/House-Music/" target="_blank">
              <video class="video" width="100%" autoplay loop muted playsinline src="https://ktut.github.io/portfolio/assets/rendered/vid-12.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-12.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>

            <a href="http://www.chicagomag.com/Chicago-Magazine/August-2018/House-Music/" class="thumb" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-12.jpg');"></a>
            
            <div class="text">
              <a href="http://www.chicagomag.com/Chicago-Magazine/August-2018/House-Music/" target="_blank">House Music</a> (Spotify integration, interactive Roland TB-303)
            </div>
          </li>

          <li>
            <a class="no-resp web-img" href="http://www.chicagomag.com/Chicago-Magazine/September-2017/How-to-Buy-Art/" target="_blank">
              <video class="video" width="100%" autoplay loop muted playsinline poster="https://ktut.github.io/portfolio/assets/rendered/vid-7-poster.jpg" src="https://ktut.github.io/portfolio/assets/rendered/vid-7.mov">
                <source src="https://ktut.github.io/portfolio/assets/rendered/vid-7.mov" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </a>
            <a href="http://www.chicagomag.com/Chicago-Magazine/September-2017/How-to-Buy-Art/" class="thumb" style="background-image: url('https://ktut.github.io/portfolio/assets/thumbs2/vid-7.jpg');"></a>
            
            <div class="text">
              <a href="http://www.chicagomag.com/Chicago-Magazine/September-2017/How-to-Buy-Art/" target="_blank">How to Buy Art</a> (responsive design using viewheight units)
            </div>
          </li>
        </ul>

      </div>
    </transition>
    
  </section>

  <section class="code" id="code">

    <br><hr><br>

    <p>I enjoy exploring new intersections of programming and design. At my current job, I’ve done a lot of work with component-based design and architecture, using Vue.js, Atomic CSS PostCSS, and various build tools.</p>

    <button class="readmore" v-on:click="toggleSection('sectionCode')">{{sectionCode.message}}</button>

    <transition name="slide-fade">
        <div v-if="sectionCode.show">

        <p>Recently I've been tasked with building programmatic design systems. Here, the developer building the page simply feeds a "card" component an array of article objects, and the component designs itself (Using a simple patterning ruleset that plucks atomic classes from an array). Fun stuff:</p>

        <p>
          <video class="lazy video" width="100%" autoplay loop muted playsinline controls src="https://ktut.github.io/portfolio/assets/rendered/fitch-1.mov">
            <source src="https://ktut.github.io/portfolio/assets/rendered/fitch-1.mov" type="video/mp4">
            Your browser does not support the video tag.
          </video>
        </p>

        <p>Here's what happens when you add this a bunch of cards, all held together with some CSS Grid:</p>

        <p style="max-width: 900px;">
          <video class="lazy video" width="100%" autoplay loop muted playsinline controls src="https://ktut.github.io/portfolio/assets/rendered/fitch-2.mov">
            <source src="https://ktut.github.io/portfolio/assets/rendered/fitch-2.mov" type="video/mp4">
            Your browser does not support the video tag.
          </video>
        </p>
        </div>
    </transition>

  </section>

  <section class="ux" id="ux">

    <br><hr><br>

    <p>My UX design philosophy is centered around streamlining the user experience, <a href="https://www.nngroup.com/articles/minimize-cognitive-load/" target="_blank">reducing cognitive load</a> and improving design.</p>

    <button class="readmore" v-on:click="toggleSection('sectionUx')">{{sectionUx.message}}</button>

    <transition name="slide-fade">
      <div v-if="sectionUx.show">
    
      <p>At <em>Chicago</em> magazine, I was tasked with overhauling our subscription page. The old page had few conversions per user, and it was clear why:</p>

      <p>
        <img src="https://ktut.github.io/portfolio/assets/purchase-old.jpg" style="width: 100%;">
      </p>

      <p>The most important, relevant and well-produced visuals (the covers) were the smallest on the page, while the most visually prominent element (the copy) wasn't even relevant to the page's primary purpose (to convert visitors into paid subscribers of the print product). Hiding the important fields in various tabs prevented the user from easily accessing them, and it wasn't even clear what order the tabs were meant to be clicked. Even our own marketing people were confused about how to use the interface.</p>

      <p>I took some time to study the in-page analytics, research current industry best practices, and talked with a few of my friends (including <a href="http://bruceackerman.com/" target="_blank">Bruce Ackerman</a>, former head of UX at <a href="https://www.avant.com/" target="_blank">Avant</a>). I settled on a simpler approach:</p>

      <p style="max-width: 900px; max-height: 675px; overflow-y: auto; border: 1px solid #bbb;">
        <img src="https://ktut.github.io/portfolio/assets/purchase-new-lg-2.jpg" style="width: 100%; vertical-align: middle;">
        <!-- <iframe src="http://web.archive.org/web/20180121131738/https://cma.pcdfusion.com/pcd/Order?iKey=I**D7B" style="width: 100%; min-height: 600px; border: 1px solid #bbb;"></iframe> -->
      </p>

      <p>Now, the call to action and the purchaseable products are front and center, and no important information is hidden from the user.</p>
      <p>After the design of the page was completed, I worked directly with our vendor to eliminate unnecessary fields and create a more linear experience between the load of the page and the click of the "Purchase" button. In the six months following the new page’s implementation, conversions per visitor went up 20%.</p>

      </div>
    </transition>

  </section>

  <section class="contact" id="contact">

    <br><hr><br>

    <p>Here are some clients I've worked with on a freelance basis (if you care about that kind of thing): ConAgra, Avant, Rag & Bone, Printavo, The Chicago Community Trust, ADA25, KNSTRCT, Chicago Public Schools, Mariano’s, Dalhousie University ...and more!</p>

    <p>You can reach me by email at <a href="mailto:ramzi@rkdvisuals.com?Subject=Saw%20your%20site%20at%20rkdvis.com" target="_top">ramzi@rkdvisuals.com</a>.</p>
  </section>
  
  </div>
</template>
