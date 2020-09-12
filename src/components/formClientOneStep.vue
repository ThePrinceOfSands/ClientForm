<template>
  <div class="formClient_1_step">
      <div class="main">Форма создания клиента</div>
      <div class="beforeString">
        <div class="string">

         <div class="row">
            <div>
              <label for="surname" class="require">Фамилия</label>
            </div>
            <div>
              <input type="text" id="surname" name="surname" placeholder="Иванов" v-model="surname">
            </div>
          </div>

          <div class="row">
            <div>
              <label for="name" class="require">Имя</label>
            </div>
            <div>
              <input type="text" id="name" name="firstname"  v-model="name" placeholder="Иван">
            </div>
          </div>

          <div class="row">
            <div>
              <label for="patronymic" class="notNec">Отчество</label>
            </div>
           <div>
              <input type="text" id="patronymic" name="lastname" placeholder="Иванович">
            </div>
          </div>

          <div class="row row__gender">
            <label for="gender" class="require">Пол</label>
            <select id="gender" class="genderSelect" v-model="gender">
              <option></option>
              <option>Муж.</option>
              <option>Жен.</option>
            </select>
          </div>
        </div>
        <div class="string string__dateAndTel">
          <div class="row">
            <div>
              <label for="date" class="require">Дата рождения</label>
            </div>
            <div>
              <input type="text" id="date" v-model="birthday" placeholder="дд/мм/гггг">
            </div>
          </div>

          <div class="row">
            <div>
              <label for="tel" class="require">Номер телефона</label>
            </div>
            <div>
              <input type="text" id="tel" name="tel" pattern="+7-([0-9]{3})-[0-9]{3}-[0-9]{2}-[0-9]{2}" placeholder="Телефон" v-model="tel">
            </div>
          </div>
        </div>
      </div>

      <div class="groupsDoctors">
        <!-- Выбор группы-->

        <div class="doctors">
          <div class="doctors__name require">Группа клиентов</div>
          <multiSelect
              :options="GroupClients"
              value-property="value"
              display-property="name"
              v-model="resultMulti"
          />
        </div>

        <!-- Выбор врача-->

        <div class="doctors">
          <div class="doctors__name require">Врач</div>
          <vSelect
              :options="namesDoctors"
              @select="optionSelect"
              :selected="selected"
          />
        </div>
      </div>

      <div class="checkbox">
        <input type="checkbox" class="checkbox__check" id="checkbox">
        <label for="checkbox" class="checkbox__text">не отправлять смс</label>
      </div>


  </div>
</template>


<script>

import vSelect from './select';
import multiSelect from "@/components/multiselect";

export default {
  name: "formClient_1_step",
  props: ['mainData'],
  components: {
    vSelect,
    multiSelect
  },

  data() {
    return {
      namesDoctors: [
        {name: 'Иванов', value: '1'},
        {name: 'Захаров', value: '2'},
        {name: 'Чернышева', value: '3'},
      ],
      selected: "",
      GroupClients: [
        {name: 'VIP', value: 1},
        {name: 'Проблемные', value: 2},
        {name: 'ОМС', value: 3},
      ],
      resultMulti: [],
      name: '',
      surname: '',
      birthday: '',
      tel:'',
      gender: '',

    }
  },

  watch: {
    name() {
      this.mainData({
        name: this.name,
      })
    },
    surname() {
      this.mainData({
        surname: this.surname,
      })
    },
    birthday() {
      this.mainData({
        birthday: this.birthday,
      })
    },
    tel() {
      this.mainData({
        tel: this.tel,
      })
    },
    gender() {
      this.mainData({
        gender: this.gender,
      })
    },
    resultMulti() {
      this.mainData({
        resultMulti: this.resultMulti,
      })
    },
    selected() {
      this.mainData({
        selected: this.selected,
      })
    }
  },

  methods: {
    optionSelect(option) {
      this.selected = option.name;
    },

    }
  }
</script>
