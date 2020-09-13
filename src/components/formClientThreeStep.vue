<template>
  <div class="passport">
    <div class="main">
      Паспорт
    </div>

    <form class="formFirst" @submit.prevent="submitHandler" novalidate>

    <div class="dataPassport">
      <div class="dataPassport__step dataPassport__step-typeDocument">

        <div class="dataPassport__step__ch">
          <div>
            <label>Тип документа</label>
          </div>
          <div class="dataPassport__step__ch__select">
            <vSelect
                :options="typePassport"
                @select="optionSelect"
                :selected="selected"
            />
          </div>
        </div>

      </div>

      <div class="dataPassport__step dataPassport__step__align">

        <div class="dataPassport__step__ch">
          <div>
            <label for="series" class="series">Серия</label>
          </div>
          <div>
            <input type="number" id="series" onKeyPress="if(this.value.length===4) return false;">
          </div>
        </div>

        <div class="dataPassport__step__ch">
          <div>
            <label for="number" class="Number">Номер</label>
          </div>
          <div>
            <input type="number" id="number" onKeyPress="if(this.value.length===6) return false;">
          </div>
        </div>

        <div class="dataPassport__step__ch">
          <div>
            <label for="whom" class="whom">Кем выдан</label>
          </div>
          <div>
            <input type="text" id="whom">
          </div>
        </div>

        <div class="dataPassport__step__ch">
          <div>
            <label for="dataIssue" class="dataIssue require">Дата выдачи</label>
          </div>
          <div>
            <input type="date"
                   id="dataIssue"
                   v-model="form.dataIssue"
                   :class="{invalid: $v.form.dataIssue.$dirty && !$v.form.dataIssue.required}"
            >

            <div class="tooltip">
              <div v-if="($v.form.dataIssue.$dirty && !$v.form.dataIssue.required)"
              >
                <small class="tooltip__right tooltip__right-fourth"
                >Пожалуйста, укажите дату получения паспорта.</small>
              </div>
            </div>

          </div>
        </div>
      </div>
    </div>

    <div class="buttonAndWarning">
      <div class="buttonAndWarning__star">
        <span>*</span> - поле обязательное для заполнения
      </div>
      <div class="buttons">
      <button class="buttons__stepBack buttons__stepBack-formThree"
              @click.prevent="nextStepBack"
      > Назад</button>

      <button class="buttons__stepForward buttons__stepForward-formThree"
              type="submit"
      > Далее</button>

      </div>
    </div>
    </form>
  </div>
</template>

<script>
import vSelect from './select';
import {required} from "vuelidate/lib/validators";

export default {
  name: "formClientThreeStep",
  props: ['nextStep', 'backStep'],
  components: {
    vSelect
  },
  data() {
    return{
      typePassport: [
        {name: 'Паспорт', value: 1},
        {name: 'Свидетельство о рождении', value: 2},
        {name: 'Вод. удостоверение', value: 3},
      ],
      selected: '',
      form: {
        dataIssue: '',
      }
    }
  },
  methods: {
    optionSelect(option) {
      this.selected = option.name;
    },
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
      dataIssue: {
        required,
      }
    }
  }
}
</script>

