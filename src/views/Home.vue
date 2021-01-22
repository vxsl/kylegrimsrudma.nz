<template>
  <div id="fullpage" >
    <div class="section">
      <div :class="'inner-section ' + mobileClass">
        <Nav :mobile="mobile" :mobileClass="mobileClass"/>
        <div id="greeting" :class="mobileClass" ref="greeting">  
          <div v-if="!mobile" id="images" ref="images" class="initial">
            <div id="img-container">
              <img id ="codeimg" src="@/assets/code.jpg" class="img-fluid">
              <div id="portrait-container">
                <div class="d-table text-left" id="portrait-overlay">
                  <p class="d-table-cell align-bottom">Portrait by <a href="http://alexahawksworth.com/">Alexa Hawksworth.</a></p>
                  <p class="d-table-cell"></p>
                </div>
                <img id ="portraitimg" src="@/assets/me_sqrx1000.jpg" class="img-fluid">
              </div>
            </div>
          </div>
          <div id="jumbo" ref="jumbo" :class="mobileClass" class="jumbotron bg-primary text-light" align="right">
            <div id="tplysource" ref="tplysource">
              <type v-pre data-type="type1">Hello workl,.</type>
              <wait v-pre>500ms</wait>
              <delete v-pre data-chars="7" data-ignore-whitespace="false"></delete>
              <wait v-pre>500ms</wait>
              <type v-pre data-type="type1">wrok.</type>
              <delete v-pre data-chars="10" data-ignore-whitespace="false"></delete>
              <wait v-pre>50ms</wait>
              <type v-pre data-type="type1">Hello world.</type>
            </div>
            <h1 id="tplydestination" ref="tplydestination" class="display-4 text-light"></h1>
            <div class="container">
              <p id="primary-sub" class="text-light">My name is Kyle Grimsrud-Manz.</p>
              <p id="secondary-sub" class="text-light">I'm in my final year of a <span id="bold">Bachelor of Computer Science</span> at Concordia University in Montreal, and I love programming.<br></p>
              <b-button id="contact-button" variant="dark" class="btn-lg" href="mailto:hi@kylegrimsrudma.nz">Feel free to reach out.</b-button>
            </div>
          </div>
          <div v-if="mobile" id="mobile-blurb">
              <div class="text-dark">
                Thanks for visiting my website! 👨‍💻<br><br>Take a look at the <a href="https://markt.kylegrimsrudma.nz">markt</a> webapp or the <a href="https://github.com/vxsl/recoverability">recoverability</a> desktop application.
              </div>
          </div>
        </div>
      </div>
    </div>
    <div v-if="!mobile" class="section second-section">
      <div>
        <div id="blurb" class="alert bg-light" role="alert">
          <p>
          Thanks for visiting my website! 👨‍💻<br><br>Take a look at the <a href="https://markt.kylegrimsrudma.nz">markt</a> webapp or the <a href="https://github.com/vxsl/recoverability">recoverability</a> desktop application.
          </p>
        </div>
        <div class="calendar bg-dark text-light"></div>
        <a class="label" href="https://github.com/Bloggify/github-calendar">Bloggify/github-calendar</a>
      </div>
    </div>
  </div>
</template>

<script src='@/assets/scripts/tply.js'>
</script>

<script>
require('@/assets/scripts/tply.js')
import Nav from '@/components/Nav.vue'
const fullpage = require('fullpage.js')
const GitHubCalendar = require('github-calendar')

export default {
  name: 'Home',
  components: {
    Nav
  },
  data() {
        return {
        }
    },
  computed: {
    mobile() {
      return screen.width <= 760? true : false
    },
    mobileClass() {
      return this.mobile? 'mobile' : null
    }
  },
  mounted() {
    if (!this.mobile) {
      const images = this.$refs.images
      const greeting = this.$refs.greeting
      var fullPageInstance = new fullpage('#fullpage', {
        onLeave() {
          images.classList.remove('initial')
          images.classList.add('leave-first-page')
          greeting.classList.add('leave-first-page')
        }
      });
      GitHubCalendar(".calendar", "vxsl", {responsive: true});
    }
    this.$nextTick(function(){
      tply.animate(
        this.$refs.tplysource,
        this.$refs.tplydestination,
        {
          "types": [
            {
              "name": "type1",
              "properties": {
                  "data-char-interval": "50ms",
                  "data-word-interval": "700ms"
              }
            },
            {
              "name": "type2",
              "properties": {
                  "data-char-interval": "200ms",
                  "data-word-interval": "700ms"
              }
            }
          ]
      });
    })

/* 
    var prevScrollpos = window.pageYOffset;
    var jumbo = this.$refs.jumbo;
    var images = this.$refs.images;
    var row = this.$refs.greeting;
    var hidden = false;
    var unhideFlag = false;

    window.addEventListener("scroll", function(){
      console.log("scroll")
      //var jumboClasses = jumbo.classList;
      var currentScrollPos = window.pageYOffset;
      console.log(window.scrollY)
      //console.log(hidden)
      if (prevScrollpos == 0 && !hidden) {
        hidden = true
        console.log("here")
        images.style.left = "140%";
        images.style.top = '-100vh';
        jumbo.style.top = "-100vh";
        jumbo.classList.remove("quick")
        images.classList.remove("quick")
        row.style.height = "0";
        setTimeout(() => {
          unhideFlag = true;
        }, 1000);
      }

      if (currentScrollPos == 0 && hidden && unhideFlag) {
        hidden = false
        row.style.height = "auto";
        jumbo.classList.add("quick")
        images.classList.add("quick")
        jumbo.style.top = "0";
        images.style.top = '0';
        images.style.left = "0";
        
      }
      prevScrollpos = currentScrollPos;
    }) */
  },
}
</script>
<style lang="scss">
@import '../../scss/custom.scss';
@import '../../scss/animations.scss';
//@import '../../scss/fullpage-custom.css';
@import '../../node_modules/fullpage.js/dist/fullpage.min.css';
@import '../../scss/GitHubCalendar-custom.scss';

#fullpage {
  transition-delay: 1s !important;
}

.fp-tableCell {
  display:flex;
  justify-content:center;
  align-items:center;
  padding:15%;
}
Nav {
  margin-bottom:1em;
}

.inner-section {
  display:inline-block;
  &.mobile {
    padding-top:1em;
  }
}

.second-section {
  display:flex;
  justify-content:center;
  text-align:right;
  a.label {
    color:theme-color('light-grey');
    text-align:right;
    margin-right:1em;
  }
}


#blurb {
  text-align:left;
  padding:2em;
  padding:1em;
  border-radius:1.2em;
  font-size:1.5em;
  a {
    color:theme-color('primary');
    font-weight:700;
  }
  p {
    margin-bottom:0;
  }
}

.calendar {
  width:100%;
  user-select: none;
  padding:1em;
  background:theme-color("less-dark");
  border-radius:1em;
  margin-bottom:0.5em;
  a {
    color:theme-color("info");
  }
  span {
    color:theme-color("light");
    &.text-muted {
      font-size:1.2em;
      color:theme-color("light") !important;
    }
  }
}

#fp-nav ul li a span {
  background:theme-color("primary") !important
}

.fp-viewing-1 {
  #nav-container .navbar {
    border-color:theme-color("light");
  }
  .nav-link {
    color:theme-color("light") !important;
  }
  #app {
    background:theme-color("primary") !important;
  }
  #fp-nav ul li a span {
    background:theme-color("light") !important
  }
} 

/* .fp-viewing-2 {
  #nav-container .navbar {
    border-color:theme-color("light");
  }
  .nav-link {
    color:theme-color("light") !important;
  }
  #app {
    background:theme-color("dark") !important;
  }
  #fp-nav ul li a span {
    background:theme-color("light") !important
  }
}  */
.quick {
  //transition: top 0.3s !important; /* Transition effect when sliding down (and up) */
  //transition: left 0.3s !important;
}
#greeting {

  &.leave-first-page {
    animation: slide-greeting-up 1s;
    -webkit-animation: slide-greeting-up 1s;
    -moz-animation: slide-greeting-up 1s;
    animation-delay:0.5s;
    -webkit-animation-delay:0.5s;
    -moz-animation-delay:0.5s;
  }
  height:100%;
  display:flex;
  &.mobile {
    display:inline-block
  }
  transition: height 0.3s;
  //transition-delay: 1s;
  transition-timing-function: linear;
  * {
    user-select:none;
  }

  #tplysource{
    display:none
  }

  #tplydestination {
    -webkit-user-select: none; /* Safari */        
    -moz-user-select: none; /* Firefox */
    -ms-user-select: none; /* IE10+/Edge */
    user-select: none; /* Standard */
    //white-space: nowrap;
    height:3em;
  }

  @keyframes blink {
    0% {
      opacity: 0;
    }

    50% {
      opacity: 1;
    }
  }

  .cursor {
    animation: blink 0.8s steps(1) infinite;
    display: inline-block;
    width: 0.05em;
    height: 1.1em;
    position:relative;
    top:.1em;    
    background-color: theme-color("light");
    border-radius:0.3em;
    margin-left: 0.2em;
  }

  #bold {
    font-weight:500;
  }

  #images {
    &.initial {
      animation: slide-images-in 1s;
      -webkit-animation: slide-images-in 1s;
      -moz-animation: slide-images-in 1s;
      animation-fill-mode: forwards !important;
      -webkit-animation-fill-mode: forwards !important;
    }
    &.leave-first-page {
      animation: slide-images-into-jumbo 0.4s;
      -webkit-animation: slide-images-into-jumbo 0.4s;
      -moz-animation: slide-images-into-jumbo 0.4s;
    }
    width:50%;
    position:relative;
    min-height:100%;
    /* transition-property: left, top;
    transition-duration: 0.4s, 0.3s;
    transition-delay: 0s, 0.4s;
    transition-timing-function: linear; */
    transition: left, right 0.5s !important;
    #img-container {

      float:right;
      height:100%;
      width:100%;
      display:flex;
      #codeimg {
        max-height:100%;
        position:relative;
        object-fit:cover;
        border-top-right-radius:0;
        border-bottom-right-radius:0;
        border-top-left-radius:3em;
        border-bottom-left-radius:3em;
      }
      #portrait-container {
        width:100%;
        height:100%;
        //display:flex;
        float:right;
        #portraitimg, #portrait-overlay {
          position:absolute;
          height:100%;
          object-fit:cover;
          border-top-right-radius:0;
          border-bottom-right-radius:0;
          border-top-left-radius:3em;
          border-bottom-left-radius:3em;
        }
        #portraitimg {
          left:25%;
          z-index:0;
        }
        #portrait-overlay {
          opacity:0;
          left:25%;
          width:100%;
          background-color:theme-color("light");
          color:theme-color("primary");
          height:100%;
          z-index:1;
          padding:10%;
          p {
            width:50% !important;
            a {
              font-weight:700;
            }
          }
          transition:opacity 0.5s;
        }
        #portrait-overlay:hover {
          opacity:0.8;
        }
      }
    }
  }

  #mobile-blurb {
    z-index:3;
    border:solid;
    border-color:theme-color('dark');
    border-width:1px;
    border-radius:1em;
    margin-top:1em;
    font-size:1.2em;
    width:100%;
    padding:1em;
    a {
      font-weight:700;
    }
  }
  #jumbo {
    min-height:100%;
    &.mobile {
      min-width:100vw;
      border-radius:1em;
      width:100vw;
      #tplydestination {
        z-index:2;
        height:2em;
      }
      .container {
        width:100%;
        bottom:0;
      }
      #primary-sub {
        font-size:1.7em;
        font-weight:400;
      }
      #secondary-sub {
        max-width:100%;
      }
    }
    
    z-index:2;
    //padding:3em !important;
    border-radius:2em;
    border-top-right-radius:1em;
    border-bottom-right-radius:1em;
    border-top-left-radius:7em;
    max-height:100%;
    margin-bottom:0px !important;
    transition: top 1s;
    transition-delay:0.4s;
    h1 {
      font-family:'Playfair Display';
    }
    #primary-sub {
      font-size:1.7em;
      font-weight:400;
    }
    #secondary-sub {
      max-width:70%;
      font-weight:300;
      font-size:1.2em;
    }
    .text-dark {
      font-size:1.1em;
      font-weight:400;
    }
    font-weight:100;
  }
  
  #contact-button {
    font-weight:300;
    font-style:italic;
    letter-spacing:-0.03em;
  }
}




</style>