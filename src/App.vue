<template>
    <div id="app">
        <a href="https://vuejs.org/" target="_blank"><img class="vue-icon" src="./assets/img/logo.png" alt="Vue icon" /></a>
        <header-component></header-component>
        <transition name="transition" @enter="enter" @leave="leave" :css="false" mode="out-in" appear>
            <router-view ref="page"></router-view>
        </transition>
    </div>
</template>

<script>

import { TweenMax } from 'gsap'

import HeaderComponent from './components/common/Header'

export default {
    name: 'app',
    methods: {
        enter(el, done) {
            this.$store.dispatch('increment')
            if (this.$refs.page.enter) this.$refs.page.enter(el, done)
            else TweenMax.to(el, 0.5, { opacity: 1, y: 0, onComplete: done })
        },
        leave(el, done) {
            if (this.$refs.page.leave) this.$refs.page.leave(el, done)
            else TweenMax.to(el, 0.5, { opacity: 0, y: 50, onComplete: done })
        }
    },
    components: {
        HeaderComponent
    },
}

</script>

<style lang="scss">
@import "~assets/css/main";
#app {
    font-family: $font-family;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    margin-top: 40px;
}
.vue-icon {
    width: 20px;
    margin-bottom:10px;
}
.fade-enter-active, .fade-leave-active {
    transition: opacity .5s
}
.fade-enter, .fade-leave-active {
    opacity: 0
}
</style>
