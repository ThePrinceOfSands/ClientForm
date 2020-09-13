<template>
  <div class="formClient_1_step">
      <div class="main">Форма создания клиента</div>

    <form class="formFirst" @submit.prevent="submitHandler" novalidate>

      <div class="beforeString">
        <div class="string">
          <!--Фамилия-->
          <div class="row">
            <div>
              <label for="surname"
                     class="require"
              >
                Фамилия</label>
            </div>
            <div>
              <input
                  type="text"
                  id="surname"
                  name="surname"
                  placeholder="Иванов"
                  :class="{ invalid: ($v.form.surname.$dirty && !$v.form.surname.required)}"
                  v-model.trim="form.surname">
            </div>

            <div class="tooltip">
              <div v-if="$v.form.surname.$dirty && !$v.form.surname.required"
              >
                <small class="tooltip__left tooltip__left-first"
                >Пожалуйста, введите свою фамилию.</small>
              </div>
            </div>
          </div>

          <!--Имя-->
          <div class="row">
            <div>
              <label for="name" class="require">Имя</label>
            </div>
            <div>
              <input type="text"
                     id="name"
                     name="firstname"
                     v-model.trim="form.name"
                     :class="{invalid: ($v.form.name.$dirty && !$v.form.name.required)}"
                     placeholder="Иван">
            </div>

            <div class="tooltip">
              <div v-if="$v.form.name.$dirty && !$v.form.name.required"
              >
                <small class="tooltip__left tooltip__left-second"
                >Пожалуйста, введите свое имя.</small>
              </div>
            </div>
          </div>

          <!--Отчество-->
          <div class="row">
            <div>
              <label for="patronymic" class="notNec">Отчество</label>
            </div>
            <div>
              <input type="text" id="patronymic" name="lastname" placeholder="Иванович">
            </div>
          </div>

          <!--Пол-->
          <div class="row row__gender">
            <label for="gender" class="require">Пол</label>

            <select id="gender"
                    class="genderSelect"
                    v-model.trim="form.gender"
                    :class="{invalid: ($v.form.gender.$dirty && !$v.form.gender.required)}"
                    value=" "
            >
              <option>Муж.</option>
              <option>Жен.</option>
            </select>

            <div class="tooltip">
              <div v-if="$v.form.gender.$dirty && !$v.form.gender.required"
              >
                <small class="tooltip__left tooltip__left-third"
                >Пожалуйста, укажите свой пол.</small>
              </div>
            </div>
          </div>
        </div>

        <div class="string string__dateAndTel">

          <!--Дата рождения-->
          <div class="row">
            <div>
              <label for="date" class="require">Дата рождения</label>
            </div>
            <div>
              <input
                  type="date"
                  id="date"
                  v-model.trim="form.birthday"
                  :class="{invalid: ($v.form.birthday.$dirty && !$v.form.birthday.required) || ($v.form.birthday.$dirty && !$v.form.birthday.minLength)}"
              >

              <div class="tooltip">
                <div v-if="($v.form.birthday.$dirty && !$v.form.birthday.required) || ($v.form.birthday.$dirty && !$v.form.birthday.minLength)"
                >
                  <small class="tooltip__right tooltip__right-first"
                  >Пожалуйста, укажите день своего рождения.</small>
                </div>
              </div>

            </div>
          </div>

          <!--Телефон-->
          <div class="row">
            <div>
              <label for="tel"
                     class="require"
              >Номер телефона</label>
            </div>
            <div>
              <input type="tel"
                     id="tel"
                     name="tel"
                     placeholder="Телефон"
                     v-model.trim="form.tel"
                     :class="$v.form.tel.$error ? 'invalid' : ''"
              >

              <div class="tooltip">
                <div v-if="($v.form.tel.$dirty && !$v.form.tel.required)"
                >
                  <small class="tooltip__right tooltip__right-second"
                  >Пожалуйста, введите номер своего телефона.</small>
                </div>

                <div v-else-if="($v.form.tel.$dirty && !$v.form.tel.integer)"
                >
                  <small class="tooltip__right tooltip__right-second tooltip__right-second-two"
                  >Пожалуйста, вводите в поле только цифры.</small>
                </div>
              </div>

            </div>
          </div>
        </div>
      </div>


      <div class="groupsDoctors">

        <!-- Выбор группы-->
        <div class="doctors">
          <div class="doctors__name require">Группа клиентов</div>
          <multiselect
              :options="GroupClients"
              value-property="value"
              display-property="name"
              v-model.trim="form.groupClient"
              :class="{invalid: $v.form.groupClient.$dirty && !$v.form.groupClient.required}"
          />

          <div class="tooltip">
            <div v-if="$v.form.groupClient.$dirty && !$v.form.groupClient.required"
            >
              <small class="tooltip__left tooltip__left-fourth"
              >
                Пожалуйста, укажите группу клиентов.</small>
            </div>
          </div>
        </div>

        <!-- Выбор врача-->
        <div class="doctors doctors__mobile">
          <div class="doctors__name require">Врач</div>
          <vSelect
              :options="namesDoctors"
              @select="optionSelect"
              :selected="form.doctor"
              v-model.trim="form.doctor"
              :class="{invalid: ($v.form.doctor.$dirty && !$v.form.doctor.required)}"
          />

          <div class="tooltip">
            <div v-if="$v.form.doctor.$dirty && !$v.form.doctor.required"
            >
              <small class="tooltip__right tooltip__right-third"
              >
                Пожалуйста, укажите желаемого врача.</small>
            </div>
          </div>
        </div>
      </div>

      <div class="checkbox">
        <input type="checkbox" class="checkbox__check" id="checkbox">
        <label for="checkbox" class="checkbox__text">не отправлять смс</label>
      </div>

    <div class="buttonAndWarning">
      <div class="buttonAndWarning__star">
        <span>*</span> - поле обязательное для заполнения
      </div>

        <button class="buttons__stepForward buttons__stepForward__formOne"
                type="submit"
        >
          Далее</button>
      </div>
    </form>
  </div>
</template>

<script>

import vSelect from './select';
import multiselect from "@/components/multiselect";
import {required, integer} from "vuelidate/lib/validators";

export default {
  name: "formClient_1_step",
  props: ['nextStep'],
  components: {
    vSelect,
    multiselect
  },
  data() {
    return {
      namesDoctors: [
        {name: 'Иванов', value: '1'},
        {name: 'Захаров', value: '2'},
        {name: 'Чернышева', value: '3'},
      ],
      GroupClients: [
        {name: 'VIP', value: 1},
        {name: 'Проблемные', value: 2},
        {name: 'ОМС', value: 3},
      ],

      form: {
        groupClient: '',
        name: '',
        surname: '',
        birthday: '',
        tel:'',
        gender: '',
        doctor: "",
      }

    }
  },

  methods: {
    optionSelect(option) {
      this.form.doctor = option.name;
      },
    stepForward() {
      this.nextStep({});
    },
    submitHandler() {
      this.$v.form.$touch();
      if (!this.$v.form.$error)
        this.stepForward();
        //console.log(1);
    },
  },
  validations: {
      form: {
        name: {
          required
        },
        surname: {
          required
        },
        gender: {
          required
        },
        birthday: {
          required,
          minLength(value) {
            return value.split('-').length === 3;
          }
        },
        tel: {
          required,
          integer,
        },
        groupClient: {
          required,
        },
        doctor: {
          required,
        }


    }
  }
}
</script>
