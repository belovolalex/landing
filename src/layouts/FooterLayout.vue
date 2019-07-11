<template>
  <footer>
    <div class="container">
      <div class="row mb-32">
        <div class="col text-center">
          <img :src="dot" alt="">
        </div>
      </div>
      <div class="row">
        <div class="col text-center">
          <h3 class="footer-title">For Queries</h3>
        </div>
      </div>
      <div class="row mb-17">
         <div class="col col-md-6 offset-md-3">
           <p class="footer-ask mb-0">Have a question to ask? Mail it to <a href="mailto:support@gmail.com" class="footer-ask-mail">support@gmail.com</a></p>
           <p class="footer-ask">and we'll get back to you</p>
         </div>
      </div>
      <div class="row">
        <div class="col text-center">
          <p class="footer-copyright">© 2018, Phycon Limited. All Rights Reserved.</p>
        </div>
      </div>
    </div>
    <div class="m-auto mb-5 text-center">
      <div class="footer-wrap-select">
        <i class="fas fa-globe-europe footer-select-icon"></i>
        <multiselect
                    v-model="value"
                    :searchable="false"
                    :allow-empty="false"
                    label="long"
                    @select="changeLang(value)"
                    :options="langs"
                    :local-search="false"
        ></multiselect>
      </div>
    </div>
  </footer>
</template>

<script>
import {langs} from '../store'
import Multiselect from 'vue-multiselect'
export default {
  components: {
    Multiselect
  },
  data() {
    return {
      dot: require('../assets/images/polygon-1.png'),
      value: [],
      langs: []
    }
  },
  mounted() {
    this.langs = langs
    this.value = this.langs[3]
  },
  methods: {
    changeLang(value) {
      console.log('value', value)
    }
  }
}
</script>
<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>
<style>
  .footer-title {
    letter-spacing: 0.75px;
    font-family: 'sans-l';
    margin-bottom: 17px;
    color: #030d1b;
    font-size: 30px;
  }
  .footer-ask {
    letter-spacing: 0.4px;
    font-family: 'sans-l';
    text-align: center;
    color: #030d1b;
    font-size: 16px;
  }
  .footer-ask-mail {
    position: relative;
    color: #0054a2;
  }
  .footer-ask-mail:hover {
    text-decoration: none;
  }
  .footer-ask-mail:before {
    position: absolute;
    background: rgba(0, 84, 162, 0.53);
    content: '';
    width: 100%;
    height: 1px;
    bottom: 0;
  }
  .footer-copyright {
    font-family: 'sans-r';
    letter-spacing: 0.35px;
    margin-bottom: 20px;
    font-size: 14px;
    color: #7e7e7e;
  }
  .mb-17 {
    margin-bottom: 17px;
  }
  .mb-32 {
    margin-bottom: 32px;
  }
  .multiselect__option--highlight {
    background: transparent !important;
  }
  .multiselect__option--highlight:after {
    content: '' !important;
  }
  .footer-wrap-select {
    display: inline-block;
    margin-bottom: 37px;
    position: relative;
  }
  .footer-select-icon {
    position: absolute;
    color: #040707;
    z-index: 9999;
    top: 7px;
    left: 6px;
  }
  .multiselect__element {
    padding-left: 17px;
  }
  .multiselect {
    box-sizing: border-box !important;
    font-family: 'sans-r' !important;
    background-color: #dedede;
    color: #040707 !important;
    font-size: 13px !important;
    border: none !important;
    padding: 0 !important;
    border-radius: 30px;
    width: 110px;
    min-height: 30px !important;
    height: 30px !important;
    margin: 0 auto;
  }
  .multiselect__placeholder {
      margin-bottom: 0 !important;
      margin-top: 5px !important;
  }
  .multiselect__single {
      font-family: 'sans-l';
      margin: 0 !important;
      background-color: transparent !important;
      font-size:13px;
      padding: 0;
      padding-left: 20px;
      padding-top: 5px;
  }
  .multiselect__option span {
    font-family: 'sans-l' !important;
  }
  .multiselect__option--selected {
    background-color: transparent !important;
  }
  .multiselect__option--selected:after {
      display: none !important;
  }
  .multiselect__option {
      font-family: 'sans-l' !important;
      color: #040707 !important;
      font-size: 13px !important;
      width: 100% !important;
  }
  .multiselect__content-wrapper {
      width: 100% !important;
  }
  .multiselect__option--highlight:after {
      content: '' !important;
  }
  .multiselect__tags {
      border: none !important;
      border-radius: 2px !important;
      background-color: transparent !important;
      padding: 0 10px 0 10px !important;
  }
  .multiselect__tags {
      min-height: 40px;
      display: block;
      padding: 8px 40px 0 8px;
      border-radius: 5px;
      border: 1px solid #e8e8e8;
      background: #fff;
      font-size: 14px;
  }
  .multiselect__select {
    width: 29px !important;
    height: 29px !important;
  }
  .multiselect__select::before {
    margin-top: initial !important;
    right: initial !important;
    border-width: initial !important;
    border-style: initial !important;
    border-color: initial !important;
    content: "‹";
    font-size: 20px;
    color: #040707;
    transform: rotate(90deg) !important;
    display: inline-block;
    top: 2px !important;
    left: 3px;
  }
</style>