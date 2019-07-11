<template>
  <section class="flyer">
    <div class="container">
      <div class="row">
        <div class="col text-center">
          <h1 class=flyer_h1>How to make flyer real?</h1>
        </div>
      </div>
      <div class="row">
        <div class="m-auto col col-lg-7 text-center">
          <h2 class="flyer_h2">Proin suscipit luctus orci placerat fringilla. Donec hendrerit laoreet risus eget adipiscing.</h2>
        </div>
      </div>
      <div class="wrapper-gif d-lg-none text-center">
        <img :src="gifImg" alt="">
      </div>
      <div class="row d-none d-lg-flex" ref="flyer">
        <div class="wrap-flyer-img m-auto">
          <img :src="flyeImg" alt="">
          <div class="row wrap-gif">            
              <img :src="activePhone ? gifImg : ''" alt="">
          </div>
          <div class="wrap-flyer-phone" :style="{left: valLeftPositionPhone + '%', top: valTopPosition + '%'}">
            <img :src="phoneImg" alt="" class="phone-img">
            <img :src="handImg" alt="" class="finger-img" @click="handleFinger">
          </div>
        </div>
      </div>
      <div class="row wrap-flyer-points d-none d-lg-flex">
          <div class="col flyer-points offset-md-4 col-lg-6">
              <div
                v-for="n in 4"
                :key="n"
                class="flyer-point"
                :class="`flyer-point-${n}`"
                @click="handleClickOnDot(n)"
              ></div>
          </div>
      </div>
      <div class="row wrap-curve-comp d-none d-lg-flex">
        <curve-comp v-on:valx="handleValX" :valCurve="clickOnFinger" :activeDot="activeDot"></curve-comp>
      </div>
      <div class="row text-center row-title-drag d-none d-lg-block">
        <div class="col offset-sm-3 col-sm-6">
          <p class="title-drag">
            <span class="fas fa-chevron-left flyer-icon-left"></span>
            drag or scroll left / right
            <span class="fas fa-chevron-right flyer-icon-right"></span>
          </p>
        </div>
      </div>
      <div class="row mb-3">
        <div class="col text-center">
          <div class="col col-md-6 col-lg-4 col-flyer-btn wrap-flyer-btn m-auto">
            <button class="btn btn-flyer">Download</button>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <p class="flyer-p mb-flyer-p">Nullam eros mi, mollis in sollicitudin non, tincidunt sed enim.</p>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
import CurveComp from './CurveComp'

export default {
  components: {
    CurveComp
  },
  data() {
    return {
      activeDot: null,
      clickOnFinger: false,
      positionPhone: -40,
      topPositionPhone: 0,
      activePhone: false,
      gifImg: require('../assets/images/dog.gif'),
      flyeImg: require('../assets/images/flyer.png'),
      handImg: require('../assets/images/ico-drag.png'),
      phoneImg: require('../assets/images/phone.png'),
    }
  },
  computed: {
    valLeftPositionPhone() {
      if(this.positionPhone < -40) {
        return -40
      }else if(this.positionPhone > -40 && this.positionPhone >= 18) {
        this.activePhone = true
        return 18
      } else {
        this.activePhone = false
        return this.positionPhone
      }
    },
    valTopPosition() {
      if(this.positionPhone < -40) {
        return 0
      }else {
        return this.topPositionPhone
      }
    }
  },
  methods: {
    changeStateActivePhone() {
      this.activePhone = !this.activePhone
    },
    handleValX(val) {
      let step = val
      let halfStep = 462/step
      let procVal = 100/halfStep
      if(step < 0) {
        this.positionPhone = -40
        this.topPositionPhone = 0
      } else if(step > 490) {
        procVal = 100
      } else {
        this.topPositionPhone = 1 -10/halfStep
        this.positionPhone = -45 + 60/halfStep
      }
    },
    handleFinger() {
      this.clickOnFinger = true
      this.$nextTick(() => this.clickOnFinger = false)
      for (let index = 0; index < 414; index++) {
        setTimeout(() => {
          this.positionPhone = index
          this.topPositionPhone = -10
        }, 0)
      }
    },
    handleClickOnDot(num) {
      this.activeDot = num
      switch (num) {
        case 1: this.positionPhone = -40, this.topPositionPhone = 0
          break;
        case 2: this.positionPhone = -23, this.topPositionPhone = -3
          break;
        case 3: this.positionPhone = 1, this.topPositionPhone = -7
          break;
        case 4: this.positionPhone = 18, this.topPositionPhone = -10
          break;
      }
      this.$nextTick(() => {
        this.activeDot = 0
      })
    }
  }
}
</script>

<style>
.wrap-flyer-points {
  margin-top: -35px;
  height: 86px;
}
.wrapper-gif {
    margin-top: 30px;
    margin-bottom: 50px;
}
.wrapper-gif img {
  width: 100%;
  max-width: 400px;
  height: auto;
}
.flyer-point {
  width: 12px;
  height: 12px;
  cursor: pointer;
  border-radius: 50%;
  position: absolute;
}
.flyer-point-1 {
  background-color: #a2a0a0;
  left: 43px;
  top: 43px;
}
.flyer-point-2 {
  background-color: #bbb9b9;
  left: 163px;
  top: 33px;
}
.flyer-point-3 {
  background-color: #c7c5c5;
  left: 283px;
  top: 40px;
}
.flyer-point-4 {
  background-color: #eaeaea;
  left: 405px;
  top: 59px;
}
.wrap-gif {
  position: absolute;
  height: 116px;
  width: 200px;
  left: 274px;
  top: 295px;
}
.wrap-gif img {
  transform: perspective(284px) rotateX(11deg);
  border-radius: 4px;
  height: 117px;
  width: 100%;
}
.phone-img {
  opacity: 0.3;
  height: 100%;
}
.wrap-curve-comp {
  justify-content: center;
  position: relative;
}
.wrap-flyer-img {
  position: relative;
  padding-bottom: 35px;
}
img.finger-img {
  position: absolute;
  bottom: 0;
  left: 214px;
  z-index: 99999;
  opacity: 1;
}
.row-title-drag {
  margin-top: -18px;
  margin-bottom: 58px;
}
.title-drag {
  text-transform: uppercase;
  font-family: 'sans-l';
  font-size: 14px;
  color: #b1b1b1;
}
.flyer-icon-left, .flyer-icon-right {
  color: #bfbfbf;
}
.flyer-icon-left {
  margin-right: 35px;
}
.flyer-icon-right {
  margin-left: 35px;
}
.flyer {
  margin-top: 50px;
}
.flyer_h1 {
  text-transform: uppercase;
  font-family: 'sans-semi';
  margin-bottom: 24px;
  color: #555555;
  font-size: 16px;
}
.flyer_h2 {
  font-family: 'sans-semi';
  margin-bottom: 20px;
  color: #00005a;
  font-size: 24px;
}
.wrap-flyer-phone {
    position: absolute;
    left: -271px;
    top: 0;
    display: none; 

}
.wrap-flyer-btn {
  background: linear-gradient(90deg, #4350ce, #a105bd);
  display: inline-block;
  border-radius: 35px;
  padding: 3px;
}
.wrap-flyer-btn:hover {
  background: linear-gradient(90deg, #a105bd, #4350ce);
}
.col-flyer-btn {
  padding-right: 3px !important;
  padding-left: 3px !important;
}

.btn.btn-flyer {
  background-color: white;
  text-transform: uppercase;
  border-radius: 35px;
  font-family: 'sans-semi';
  color: #722ac5;
  font-size: 30px;
  width: 100%;
}
.btn.btn-flyer:hover {
  color: #8828b5;
}
.flyer-p {
  font-family: 'sans-r';
  text-align: center;
  color: #9b9b9b;
  font-size: 14px;
}
.mb-flyer-p {
  margin-bottom: 50px;
}

@media (min-width: 992px) {
  .wrap-flyer-phone {
    display: initial;
    left: -271px;
  }
  .flyer_h2 {
    margin-bottom: 70px;
  }
  .wrap-flyer-img {
    margin-bottom: 0;
  }
  
}
</style>
