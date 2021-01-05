<template>
  <div id="app">
    <div id="nav">
      <b-navbar  fixed="top" type="light" variant="light">
        <b-navbar-nav>
          <b-nav-item href="/resume">Resumé</b-nav-item>
          <b-nav-item href="https://github.com/vxsl">Github</b-nav-item>
          <b-nav-item href="#">LinkedIn</b-nav-item>
        </b-navbar-nav>
      </b-navbar>
    </div>
    <router-view/>
  </div>
</template>

<style lang="scss">
  @import '../scss/custom.scss';
  @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,800;1,600&display=swap');
  @import url('https://fonts.googleapis.com/css2?family=Inconsolata:wght@200;300;400&display=swap');
</style>

<style lang="scss">

#app {
  font-family: Inconsolata, Courier, monospace;
  letter-spacing:0.001em;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

#nav {
  padding: 30px;

  a {
    //font-weight: bold;
    //color: #2c3e50;

    &.router-link-exact-active {
      //color: #42b983;
    }
  }
}
</style>
