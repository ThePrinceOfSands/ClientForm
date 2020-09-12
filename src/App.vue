<template>
  <div id="app">
    <div class="window">

      <form novalidate>
        <formClientOneStep
            v-show="step === 1"
            :mainData="changeData"
        />

        <formClientTwoStep
            v-show="step === 2"
            :mainData="changeData"
        />

        <formClientThreeStep
            v-show="step === 3"
            :mainData="changeData"
        />

        <formClientFourStep
            v-show="step === 4"
        />
      </form>

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
//import { required, minLength } from 'vuelidate/lib/validators';


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
      step: 1,
      formReg: {
        name: '',
        surname: '',
        birthday: '',
        tel: '',
        gender: '',
        selected: '',
        town: '',
        dataIssue: '',

      }
    }
  },

  methods: {
    nextStep() {
      if(this.step < 4)
        this.step++;
      //console.log(this.step);
    },
    backStep() {
      if(this.step > 1)
        this.step--;
      //console.log(this.step);
    },
    changeData(data) {
      let keys = Object.keys(data);
      this.formReg[keys] = data[keys];
      console.log(this.formReg);
    }

  }
}
</script>

