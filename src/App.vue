<template>
  <div id="app" class="bg-light">
      <div id="nav-container" fixed="top">
        <b-navbar id="nav">
          <b-navbar-nav id="left-items">
            <b-nav-item href="https://github.com/vxsl">Github</b-nav-item>
            <b-nav-item href="https://www.linkedin.com/in/kyle-grimsrud-manz-0b0624203/">LinkedIn</b-nav-item>
          </b-navbar-nav>

          <b-navbar-nav class="ml-auto" id="right-items">
            <b-nav-item href="mailto:hi@kylegrimsrudma.nz" right>hi@kylegrimsrudma.nz</b-nav-item>
          </b-navbar-nav>
        </b-navbar>
      </div>
    <router-view/>
  </div>
</template>

<style lang="scss">
@import '../scss/custom.scss';
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,800;1,600&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Inconsolata:wght@200;300;400;500;700&display=swap');

#app {
  font-family: Inconsolata, Courier, monospace;
  letter-spacing:0.001em;
  text-align: center;
  transition: background 1s;
}
#right-items {
  float:right;
  text-align:right;
  font-weight:700;
}
#nav-container {
  position:absolute;
  z-index:4;
  width:100%;
  padding-left:16% !important;
  padding-right:16% !important;
  padding-top:1.2em;
  padding-bottom:1.2em;
  .navbar {
    border:solid;
    border-color:theme-color("primary");
    border-radius:1em;
    border-width:1px;
  }
}

.nav-link {
  color:theme-color("primary") !important;
}

a:hover {
  font-weight:700;
}
</style>
