<template>

  <div id="fullpage">
    <div class="section">
      <div :class="'inner-section ' + mobileClass">
        <Nav :mobile="mobile" :mobileClass="mobileClass"/>
        <div id="greeting" :class="mobileClass" ref="greeting">  
          <div v-if="!mobile" id="images" ref="images">
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
        </div>
        <div id="jumbo" ref="jumbo" :class="mobile? 'mobile' : 'col-5'" class="jumbotron bg-primary text-light" align="right">
          <div class="container">
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
            <p id="primary-sub" class="text-light">My name is Kyle Grimsrud-Manz.</p>
            <p id="secondary-sub" class="text-light">I'm in my final year of a <span id="bold">Bachelor of Computer Science</span> at Concordia University in Montreal, and I love programming.<br></p>
            <b-button id="contact-button" variant="dark" class="btn-lg" href="mailto:hi@kylegrimsrudma.nz">Feel free to reach out.</b-button>
          </div>
        </div>
        <div class="col-2"></div>
      </b-row>
    </div>
    <div class="section">
      <b-row class="d-flex justify-content-center">
        <b-container fluid id="blurb">
          <b-col>
            <div class="alert align-middle alert-primary bg-light" role="alert">
              Thanks for visiting my website! 👨‍💻<br><br>Take a look at the <a href="https://markt.kylegrimsrudma.nz">markt</a> webapp or the <a href="https://github.com/vxsl/recoverability">recoverability</a> desktop application.
            </div>
            <p class="text-light">Otherwise, you can scroll down for a summary of my personal work.</p>
          </b-col>
        </b-container>
      </b-row>
    </div>
    <div class="section summary-section">
      <div class="d-flex justify-content-center">
        <div class="calendar text-light"></div>
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
      var fullPageInstance = new fullpage('#fullpage', {
        navigation: true,
        paddingTop: '3em',
        //sectionsColor:['#ff5f45', '#0798ec', '#fc6c7c', 'grey']
      });
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

        GitHubCalendar(".calendar", "vxsl", {responsive: true});

        var prevScrollpos = window.pageYOffset;
        var jumbo = this.$refs.jumbo;
        var images = this.$refs.images;
        var row = this.$refs.greeting;
        var hidden = false;
        var unhideFlag = false;

        window.scroll(() => {
          console.log("HERE")
        })

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
        })
      })
    },
}
</script>

<style lang="scss">
@import '../../scss/custom.scss';
@import '../../scss/fullpage-custom.css';
@import '../../scss/GitHubCalendar-custom.scss';

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

.summary-section {
  padding-left:20%;
  padding-right:20%;
  .calendar {
    user-select: none;
    width:100%;
    padding:1em;
    background:theme-color("less-dark");
    border-radius:1em;
    a {
      color:theme-color("info");
    }
    span {
      color:theme-color("light");
      &.text-muted {
        color:theme-color("light") !important;
      }
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

.fp-viewing-2 {
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
} 
.quick {
  transition: top 0.3s !important; /* Transition effect when sliding down (and up) */
  //transition: left 0.3s !important;
}
#greeting {

  display:flex;
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
    height:4em;
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

  .col-3 {
    padding:0;
    overflow:visible !important;
  }

  #bold {
    font-weight:500;
  }

  #images {
    position:relative;
    height:100%;
    transition-property: left, top;
    transition-duration: 0.4s, 0.3s;
    transition-delay: 0s, 0.4s;
    transition-timing-function: linear;

    #img-container {
      float:right;
      height:100%;
      display:flex;
      #codeimg {
        width:100%;
        position:relative;
        object-fit:cover;
        border-top-right-radius:0;
        border-bottom-right-radius:0;
        border-top-left-radius:3em;
        border-bottom-left-radius:3em;
      }
      #portrait-container {
        display:flex;
        float:right;
        height:100%;
        #portraitimg, #portrait-overlay {
          width:100%;
          position:absolute;
          object-fit:cover;
          border-top-right-radius:0;
          border-bottom-right-radius:0;
          border-top-left-radius:3em;
          border-bottom-left-radius:3em;
        }
        #portraitimg {
          height:100%;
          left:25%;
          z-index:0;
        }
        #portrait-overlay {
          opacity:0;
          left:25%;
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

  #jumbo {
    &.mobile {
    }
    z-index:2;
    padding:3em !important;
    display:flex;
    border-radius:2em;
    top: 0; /* Stay on top */
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


#blurb {
  margin:2em;
  max-width:50%;
  .alert {
    padding:1em;
    border-radius:1.2em;
    font-size:1.5em;
    a {
      color:theme-color('primary');
      font-weight:700;
    }
  }
  p {
    font-size:1.2em;
  }
}
</style>
