<template>
  <b-container fluid class="bg-light">
    <b-row id="greeting">
      <div id="portrait" ref="portrait" class="col-6 img-fluid"></div>
      <div id="jumbo" ref="jumbo" class="col-6 jumbotron bg-info text-light" align="right">
        <div class="container primary ">
          <div id="tplysource" ref="tplysource">
            <type>Hello World.</type>
          </div>
          <h1 id="tplydestination" ref="tplydestination" class="display-4 text-primary"></h1>
          <p class="lead"></p>
          <p class="lead">My name is Kyle Grimsrud-Manz</p>
          <p class="text-muted">I'm polishing off a Bachelor of Computer Science at Concordia University in Montreal<br>(Minor in Philosophy).</p>
          <b-button id="contact" variant="dark" class="btn-lg" href="#">Feel free to reach out.</b-button>
        </div>
      </div>
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
            images: {
                portrait: require('@/assets/me_sqr.jpg')
            }
        }
    },
  mounted() {
      this.$nextTick(function(){
        tply.animate(
          this.$refs.tplysource,
          this.$refs.tplydestination,
          {
            types: {
                name: "robot-type",
                properties: {
                    "data-char-interval": "0ms",
                    "data-comma-interval": "0ms",
                    "data-period-interval": "0ms",
                    "data-word-interval": "100ms"
                },
            },
            processing: {
                tag: "div",
                pre: function(element) {
                    element.innerText += " haha"
                },
                post: function(element) {
                    element.parentElement.style.backgroundColor = "red";
                }
            }
        });
        var prevScrollpos = window.pageYOffset;
        var jumbo = this.$refs.jumbo;
        var portrait = this.$refs.portrait;
        window.addEventListener("scroll", function(){
          //var jumboClasses = jumbo.classList;
          var currentScrollPos = window.pageYOffset;
          if (prevScrollpos > currentScrollPos) {
            jumbo.style.top = "0px";
            portrait.style.top = "0px";
            jumbo.classList.toggle("quick")

          } else {
            jumbo.style.top = "-100em";
            portrait.style.top = "-100em";
            jumbo.classList.toggle("quick")

          }
          prevScrollpos = currentScrollPos;
          
        })
      })
    },
}
</script>



<style lang="scss">

.quick {
  background-color:red !important;
  transition: top 0.3s; /* Transition effect when sliding down (and up) */
}



#greeting {

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
  

  padding-top:2em;
  #portrait {
    top: 0; /* Stay on top */
    width: 100%; /* Full width */
    transition: top 0.3s; /* Transition effect when sliding down (and up) */
    background:#FCFCFC;
    background-image:url(../assets/me_sqr.jpg);
    background-blend-mode:darken;
    background-size:contain;
  }

  #jumbo {
    top: 0; /* Stay on top */
    width: 100%; /* Full width */
    transition: top 3s; /* Transition effect when sliding down (and up) */
    h1 {
      font-family:'Playfair Display';
    }
    font-weight:100;
  }
}

#contact {
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
