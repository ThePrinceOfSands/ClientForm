<template>
  <div id="app">
    <div class="window">
      <formClientOneStep
          v-show="step === 1"
      />

      <formClientTwoStep
          v-show="step === 2"
      />

      <formClientThreeStep
          v-show="step === 3"
      />

      <formClientFourStep
          v-show="step === 4"
      />

      <div class="buttonAndWarning">
        <div
            v-show="step !== 4"
        >
          <span>*</span> - поле обязательное для заполнения
        </div>

        <div class="buttons">
          <button class="buttons__stepBack"
                  @click="backStep"
                  v-show="step !== 1"
          >
            Назад</button>

          <button class="buttons__stepForward"
                  @click="nextStep"
                  v-show="step !== 4"
          >
            Далее</button>
        </div>
      </div>

      <div class="dots">
        <div class="dots__dot"
             :class="{'dots__dot-active': step === 1}"
        ></div>

        <div class="dots__dot"
             :class="{'dots__dot-active': step === 2}"
        ></div>

        <div class="dots__dot"
             :class="{'dots__dot-active': step === 3}"
        ></div>

        <div class="dots__dot"
             :class="{'dots__dot-active': step === 4}"
        ></div>
      </div>

    </div>>
  </div>
</template>

<script>

import formClientOneStep from '@/components/formClientOneStep';
import formClientTwoStep from '@/components/formClientTwoStep';
import formClientThreeStep from '@/components/formClientThreeStep';
import formClientFourStep from '@/components/formClientFourStep';

export default {
  name: 'app',
  components: {
    formClientOneStep,
    formClientTwoStep,
    formClientThreeStep,
    formClientFourStep,
  },
  data() {
    return {
      step: 3,
    }
  },

  methods: {
    nextStep() {
      this.step++;
      //console.log(this.step);
    },
    backStep() {
      this.step--;
      //console.log(this.step);
    },


  }
}
</script>

<style>
.buttonAndWarning {
  margin-left: 48px;
}

.buttonAndWarning span{
  color: red;
}

.buttons{
  position: relative;
}

.buttons__stepBack{
  position: absolute;
  width: 100px;
  height: 50px;
  font-size: 18px;
  background-color: #fff;
  cursor: pointer;
  left: -5%;
  top: calc(50% + 38px);
  border: 0 solid;
  box-shadow: inset 0 0 20px rgba(255, 255, 255, 0);
  text-shadow: none;
  -webkit-transition: all 1250ms cubic-bezier(0.19, 1, 0.22, 1);
  transition: all 1250ms cubic-bezier(0.19, 1, 0.22, 1);
  outline: rgba(255, 255, 255, 0.5) solid 1px;
  outline-offset: 0;
}

.buttons__stepBack:hover {
  border: 1px solid;
  box-shadow: inset 0 0 20px rgba(255, 255, 255, 0.5), 0 0 20px rgba(255, 255, 255, 0.2);
  outline-offset: 15px;
  outline-color: rgba(255, 255, 255, 0);
  text-shadow: 1px 1px 2px #427388;
}

.buttons__stepBack:active {
  box-shadow: 0 3px 6px #000000;
  -webkit-transform: scale(0.98);
  transform: scale(0.98);
}

.buttons__stepForward{
  position: absolute;
  width: 100px;
  height: 50px;
  background-color: #fff;
  cursor: pointer;
  left: calc(50% + 150px);
  font-size: 18px;
  top: calc(50% + 37px);
  border: 0 solid;
  box-shadow: inset 0 0 20px rgba(255, 255, 255, 0);
  text-shadow: none;
  -webkit-transition: all 1250ms cubic-bezier(0.19, 1, 0.22, 1);
  transition: all 1250ms cubic-bezier(0.19, 1, 0.22, 1);
  outline: rgba(255, 255, 255, 0.5) solid 1px;
  outline-offset: 0;
}

.buttons__stepForward:hover {
  border: 1px solid;
  box-shadow: inset 0 0 20px rgba(255, 255, 255, 0.5), 0 0 20px rgba(255, 255, 255, 0.2);
  outline-offset: 15px;
  outline-color: rgba(255, 255, 255, 0);
  text-shadow: 1px 1px 2px #427388;
}

.buttons__stepForward:active {
  box-shadow: 0 3px 5px #000000;
  -webkit-transform: scale(0.98);
  transform: scale(0.98);
}
</style>