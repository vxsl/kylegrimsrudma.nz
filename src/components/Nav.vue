<template>
    <div id="nav-container" :class="mobileClass">
        <b-navbar id="nav">
            <b-navbar-nav id="left-items">  
            <b-nav-item href="https://github.com/vxsl">Github</b-nav-item>
            <b-nav-item href="https://www.linkedin.com/in/kyle-grimsrud-manz-0b0624203/">LinkedIn</b-nav-item>
            </b-navbar-nav>

            <b-navbar-nav class="ml-auto" id="right-items">
            <b-nav-item href="mailto:hi@kylegrimsrudma.nz" right>{{mobile? 'Contact' : 'hi@kylegrimsrudma.nz'}}</b-nav-item>
            </b-navbar-nav>
        </b-navbar>
    </div>
</template>

<script>
export default {
    props: {
        mobile: Boolean,
        mobileClass: String
    },
}
</script>

<style lang="scss" scoped>
@import '../../scss/custom.scss';


#nav-container {
    z-index:4;
    /* padding-left:16% !important;
    padding-right:16% !important;
    padding-bottom:1.2em; */
    .navbar {
        border:solid;
        border-color:theme-color("primary");
        border-radius:0.4em;
        border-width:1px;
    }
    #right-items {
        float:right;
        text-align:right;
        font-weight:700;
    }
}

.nav-link {
    color:theme-color("primary") !important;
}
a:hover {
  font-weight:700;
}
</style>