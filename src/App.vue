<template>
  <div id="app" class="bg-light">
    <router-view/>
  </div>
</template>

<script>
export default {
  data() {
    return {
    }
  },
  computed: {
    mobile() {
      return screen.width <= 760? true : false
    },
    mobileClass() {
      if (this.mobile) {
        return 'mobile'
      }
      else {
        return ''
      }
    }
  },
}
</script>

<style lang="scss">
@import '../scss/custom.scss';
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,800;1,600&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Inconsolata:wght@200;300;400;500;700&display=swap');
#app {
  font-family: Inconsolata, Courier, monospace;
  letter-spacing:0.001em;
  text-align: center;
  transition: background 1s;
  min-height: 100vh;
}
</style>
