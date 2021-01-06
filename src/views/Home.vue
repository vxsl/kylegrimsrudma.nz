<template>
  <b-container fluid class="bg-light">
    <b-row id="greeting" class="d-flex">
      <div class="col-2"></div>
      <div class="col-3">
        <div id="img-container">
          <img id ="codeimg" ref="code" src="@/assets/code.jpg" class="img-fluid">
          <img id ="portraitimg" ref="portrait" src="@/assets/me_sqrx1000.jpg" class="img-fluid">
        </div>
        <!--<div class="overlay">Portrait by Alexa Hawksworth.</div>-->
      </div>
      <div id="jumbo" ref="jumbo" class="col-5 jumbotron bg-primary text-light" align="right">
        <div class="container">
          <div id="tplysource" ref="tplysource">
            <type data-type="type1">Hello workl,.</type>
            <wait>500ms</wait>
            <delete data-chars="7" data-ignore-whitespace="false"></delete>
            <wait>500ms</wait>
            <type data-type="type1">wrok.</type>
            <delete data-chars="10" data-ignore-whitespace="false"></delete>
            <wait>50ms</wait>
            <type data-type="type1">Hello world.</type>
          </div>
          <h1 id="tplydestination" ref="tplydestination" class="display-4 text-light"></h1>
          <p class="lead text-light">My name is Kyle Grimsrud-Manz.</p>
          <p class="text-dark">I'm finishing my Bachelor of Computer Science<br>at Concordia University in Montreal<br></p>
          <b-button id="contact-button" variant="dark" class="btn-lg" href="#">Feel free to reach out.</b-button>
        </div>
      </div>
      <div class="col-2"></div>
    </b-row>

    <b-row >
      <b-container fluid id="blurb">
        <b-col align-self="center">
          <div class="alert align-middle alert-primary" role="alert">
            A simple primary alert—check it out!
          </div>
        </b-col>
      </b-container>
    </b-row>

    <b-row>
      <b-col>
        <b-card
          title="bnnbloomberg-markets-scraper"
          img-src="https://picsum.photos/600/300/?image=25"
          img-alt="Image"
          img-top
          tag="article"
          style="max-width: 20rem;"
          class="mb-2"
        >
          <b-card-text>
            Some quick example text to build on the card title and make up the bulk of the card's content.
          </b-card-text>

          <b-button href="#" variant="primary">Go somewhere</b-button>
        </b-card>
      </b-col>
    </b-row>
  </b-container>
</template>

<script src='@/assets/scripts/tply.js'>
</script>

<script>

require('@/assets/scripts/tply.js')
// @ is an alias to /src

export default {
  name: 'Home',
  components: {
  },
  data() {
        return {
        }
    },
  mounted() {
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
        var prevScrollpos = window.pageYOffset;
        var jumbo = this.$refs.jumbo;
        var portrait = this.$refs.portrait;
        window.addEventListener("scroll", function(){
          //var jumboClasses = jumbo.classList;
          var currentScrollPos = window.pageYOffset;

          if (prevScrollpos == 0) {
            portrait.style.left = "140%";
            portrait.style.top = '-100vh';
            jumbo.style.top = "-100vh";
            jumbo.classList.remove("quick")
            portrait.classList.remove("quick")
          }

          if (currentScrollPos == 0) {
            jumbo.classList.add("quick")
            portrait.classList.add("quick")
            jumbo.style.top = "0";
            portrait.style.top = '0';
            portrait.style.left = "20%";
          }

          /* if (prevScrollpos > currentScrollPos) {
            jumbo.style.top = "0px";
            portrait.style.top = "0px";
            jumbo.classList.toggle("quick")

          } else {
            jumbo.style.top = "-100em";
            portrait.style.top = "-100em";
            jumbo.classList.toggle("quick")

          } */
          prevScrollpos = currentScrollPos;
          
        })
      })
    },
}
</script>



<style lang="scss">
@import '../../scss/custom.scss';

.quick {
  transition: top 0.3s !important; /* Transition effect when sliding down (and up) */
  //transition: left 0.3s !important;
}

#greeting {

  display:flex;
  padding-top:2em;

  #tplysource{
    display:none
  }

  #tplydestination {
    -webkit-user-select: none; /* Safari */        
    -moz-user-select: none; /* Firefox */
    -ms-user-select: none; /* IE10+/Edge */
    user-select: none; /* Standard */
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
    //padding-left:1em;
    //width:1px !important;
    animation: blink 0.8s steps(1) infinite;
    //color: theme-color("primary") !important;
    display: inline-block;
    width: 0.05em;
    height: 1.1em;
    position:relative;
    top:.1em;    
    //background-color: red;
    background-color: blue;
    border-radius:0.3em;
    margin-left: 0.2em;
  }

  .overlay {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    height: 100%;
    width: 100%;
    opacity: 0;
    transition: .5s ease;
    background-color: #008CBA;
  }

  .col-3 {
    padding:0;
    overflow:visible !important;
  }

  #img-container {
    float:right;
    height:100%;
    display:flex;
    img {
      width:100%;
      position:relative;
      object-fit:cover;
      border-top-right-radius:0;
      border-bottom-right-radius:0;
      border-top-left-radius:3em;
      border-bottom-left-radius:3em;
    }
  }

  #portraitimg {
    left:-80%;
    transition-property: left, top;
    transition-duration: 0.15s, 0.3s;
    transition-delay: 0s, 0.25s;
    transition-timing-function: linear;
  }

  #portraitimg:hover .overlay{
    overflow:visible !important;
    opacity:1
  }

  #jumbo {
    padding:3em !important;
    display:flex;
    border-radius:2em;
    top: 0; /* Stay on top */
    max-height:100%;
    margin-bottom:0px !important;
    transition: top 1s;
    transition-delay:0.25s;
    h1 {
      font-family:'Playfair Display';
    }
    .lead {
      font-size:1.7em;
    }
    .text-dark {
      font-size:1.1em;
      font-weight:400;
    }
    font-weight:100;
  }
}

#contact-button {
  font-weight:300;
  font-style:italic;
  letter-spacing:-0.03em;
}

#blurb {
  padding:1em;
  .alert {
    margin-bottom:0 !important;
  }
}
</style>
