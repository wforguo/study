<template>
    <div id="app">
        <NavBar
            :title="routeName"
            :left-text="showBack ? '返回' : ''"
            :left-arrow="showBack"
            @click-left="handleNavHome"
        />
        <keep-alive>
            <router-view></router-view>
        </keep-alive>
        <div class="fixed-button" v-show="showBack">
            <Icon name="wap-home-o" size="32" @click="handleNavHome" />
        </div>
    </div>
</template>

<script>

import { mapActions } from "vuex";
import { Icon, NavBar } from 'vant';

export default {
    name: 'App',
    components: {
        Icon,
        NavBar
    },
    methods: {
        ...mapActions('router', [
            'setRouters'
        ]),
        handleNavHome () {
            this.$router.replace({
                path: '/',
            });
        }
    },
    computed: {
        routeName () {
            return this.$route.meta.title
        },
        showBack () {
            return this.$route.path !== '/'
        }
    },
    mounted() {
        this.setRouters({
            routers: this.$router.options.routes
        });
    }
}
</script>

<style lang="less">
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}

body {
    width: 100%;
    height: 100%;
    overflow-y: auto;
    background: linear-gradient(to top right, #ffcc00 50%, #eee 50%) no-repeat;
    background-size: 100% calc(100% - 100vh + 5px);
    position: relative;

    &:after {
        left: 0;
        top: 5px;
        bottom: 0;
        right: 0;
        position: fixed;
        content: '';
        overflow: hidden;
        background: #fff;
        z-index: -1;
    }
}

.fixed-button {
    position: fixed;
    bottom: 50px;
    right: 50px;
}
</style>
