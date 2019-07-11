<template>
<header class="header">
    <div class="container">
        <div class="row">
            <div class="wrap-navbar col">
                <nav class="navbar navbar-expand-lg navbar-light">
                    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                        <span class="navbar-toggler-icon"></span>
                    </button>

                    <div class="collapse navbar-collapse" id="navbarSupportedContent">
                        <ul class="navbar-nav mr-auto navbar-nav-header ">
                            <li class="nav-item nav-item-header" v-for="(item, idx) in routes" :key="idx">
                                <router-link
                                    :to="item.url"
                                    :class="['nav-link', 'nav-link-header']"
                                > {{ item.title }}
                            </router-link>
                            </li>
                        </ul>
                    </div>
                </nav>
            </div>
            <div class="header-settings col d-flex justify-content-end flex-column flex-md-row">
                <div class="os justify-content-end mb-1">
                    <span class="os-title">for</span>
                    <span :class="['os-item', activeOs === 1 ? 'os-item--active': '']" @click="changeActiveOsId(1)">ios</span>
                    <span :class="['os-item', activeOs === 2 ? 'os-item--active': '']" @click="changeActiveOsId(2)">android</span>
                </div>
                <ul class="header-langs d-flex justify-content-end">
                    <li class="header-lang"
                        v-for="(item, idx) in langs"
                        :key="idx"
                        @click="changeActiveLangId(item.id)"
                    >
                        <span :class="['header-lang-title', activeLang === item.id ? 'header-lang-title--active' : '']">{{ item.short }}</span>
                    </li>
                </ul>
            </div>
        </div>
        <div class="row">
            <div class="header-wrap-photo">
                <img :src="logoImg" alt="">
            </div>
        </div>
    </div>
    </header>
</template>
<script>
import {langs} from '../store'
export default {
  data() {
      return {
          logoImg: require('../assets/images/logo.png'),
          langId: 4,
          osId: 2,
          langs: [],
          routes: [
            {
                title: 'collaborations',
                url: '/collaborations'
            },
            {
                title: 'api',
                url: '/api'
            },
            {
                title: 'T&C',
                url: '/ts'
            }
          ]
      }
  },
  mounted() {
      this.langs = langs
  },
  computed: {
      activeLang() {
          return this.langId
      },
      activeOs() {
          return this.osId
      }
  },
  methods: {
    changeActiveLangId(id) {
        this.langId = id
    },
    changeActiveOsId(id) {
        this.osId = id
    }
  }
}
</script>

<style>
    .navbar {
        padding-left: 0 !important;
    }
    .header {
        margin-top: 80px;
    }
    .header-wrap-photo {
        width: 55px;
        position: absolute;
        left: 50%;
        top: 30px;
        transform: translateX(-50%);
    }
    .header-wrap-photo img {
        width: 100%;
    }
    .nav-item-header {
        position: relative;
    }
    .nav-item-header .nav-link-header {
        color: #555555 !important;
        text-transform: uppercase;
        font-family: 'sans-semi';
        font-size: 16px;
    }
    .navbar-nav-header {
        margin-top: 30px;
    }
    .header-lang-title {
        text-transform: uppercase;
        font-family: 'sans-semi';
        color: #555555;
        font-size: 18px;
        margin-left: 10px;
    }
    .header-lang-title--active {
        position: relative;
        font-family: 'sans-b';
        font-size: 21px;
        color: #00005a;
    }
    .header-lang {
        width: 35px;
    }
    .header-lang-title--active:before {
        position: absolute;
        content: '';
        background: url("../assets/images/polygon-1.png") no-repeat;
        width: 12px;
        height: 12px;
        top: 29px;
        left: 8px;
    }
    .header-settings {
        position: absolute !important;
        width: 200px !important;
        margin-right: 2px;
        top: 120px;
        right: 0;
    }
    .os {
        text-transform: uppercase;
        margin-right: -13px;
        align-items: center;
        margin-top: 3px;
        font-size: 16px;
        display: flex;
    }
    .os-title {
        font-family: 'sans-l';
        margin-right: -5px;
    }
    .os-item {
        position: relative;
        font-family: 'sans-semi';
        margin: 0 10px;
    }
    .os-item--active {
        color: #499641;
    }
    .os-item--active:after {
        background-color: #499641 !important;
    }
    .os-item:before {
        position: absolute;
        color: black;
        content: '•';
        right: -13px;
        top: 0;
    }
    .os-item:last-child:before {
        content: '';
    }
    .os-item:after {
        position: absolute;
        background-color: black; 
        content: '';
        width: 100%;
        height: 1px;
        bottom: 0;
        left: 0;
    }
    .header-langs {
        list-style-type: none;
        align-items: center;
        margin-bottom: 0;
        padding-left: 0;
    }
    .wrap-navbar {
        margin-top: 40px;
    }
    @media (min-width: 576px) {
        .header-settings {
            right: 9%;
        }
        .header-wrap-photo {
            width: 70px;
        }
    }
    @media (min-width: 992px) {
        .header {
            margin-top: 130px;
        }
        .header-lang {
            cursor: pointer;
        }
        .header-settings {
            position: static !important;
            margin-top: 30px;
            margin-right: 13px; 
        }
        .header-wrap-photo {
            margin: -115px auto 0;
            position: static;
            transform: none;
            left: auto;
            width: auto;
        }
        .header-wrap-photo img {
            width: auto;
        }
        .nav-item-header:after {
            position: absolute;
            color: #555555;
            content: '•';
            right: -3px;
            top: 21%;
        }
        .nav-item-header:last-child:after {
            content: '' !important;
        }
        .os {
            margin-right: 30px;
        }
        .os-item {
            cursor: pointer;
        }
        .wrap-navbar {
            margin-top: 0;
        }
    }
</style>