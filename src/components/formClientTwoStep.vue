<template>
  <div class="formClientTwoStep">
    <div class="main">
      Адрес
    </div>

    <form class="formFirst" @submit.prevent="submitHandler" novalidate>

    <div class="address">
      <!--Первая колона-->

      <div class="address__step1">
        
        <div class="address__step">
          <div>
            <label for="index" class="index">Индекс</label>
          </div>
          <div>
            <input type="number" id="index" onKeyPress="if(this.value.length===6) return false;">
          </div>
        </div>

        <div class="address__step">
          <div>
            <label for="region" class="region">Область</label>
          </div>
          <div>
            <input type="text" id="region">
          </div>
        </div>

        <div class="address__step">
          <div>
            <label for="street" class="street">Улица</label>
          </div>
          <div>
            <input type="text" id="street" >
          </div>
        </div>
        
        <div class="address__step">
          <div>
            <label for="house" class="house">Дом</label>
          </div>
          <div>
            <input type="number" id="house">
          </div>
        </div>
        
      </div>

      <!-- Вторая колона-->

      <div class="address__step2">
        
        <div class="address__step">
          <div>
            <label for="country" class="town">Страна</label>
          </div>
          <div>
            <input type="text" id="country" required>
          </div>
        </div>
        
        <div class="address__step">
          <div>
            <label for="town" class="town require">Город</label>
          </div>

          <div>
            <input type="text"
                   id="town"
                   v-model.trim="form.town"
                   :class="{invalid: $v.form.town.$dirty && !$v.form.town.required}"
            >

            <div class="tooltip">
              <div v-if="($v.form.town.$dirty && !$v.form.town.required)"
              >
                <small class="tooltip__right tooltip__right-second"
                >Пожалуйста, укажите Ваш город.</small>
              </div>
            </div>

          </div>
        </div>
      </div>
    </div>

    <div class="buttonAndWarning">
      <div >

        <span>*</span> - поле обязательное для заполнения </div>

      <div class="buttons">
        <button class="buttons__stepBack"
                @click.prevent="nextStepBack"
        > Назад</button>

        <button class="buttons__stepForward"
                type="submit"
        >
          Далее</button>

      </div>
    </div>
    </form>
  </div>
</template>

<script>
import {required} from "vuelidate/lib/validators";

export default {
  name: "formClientTwoStep",
  props: ['nextStep', 'backStep'],

  data() {
    return {
      form: {
        town: '',
      }
    }
  },
  methods:{
    nextStepForward() {
      this.nextStep({});
    },
    nextStepBack(){
      this.backStep({});
    },
    submitHandler() {
      this.$v.form.$touch();
      if (!this.$v.form.$error)
        this.nextStepForward();
    },
  },
  validations:{
    form: {
      town: {
        required,
      }
    }
  }
}
</script>
