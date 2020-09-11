<template>
  <div class="passport">
    <div class="main">
      Паспорт
    </div>

    <div class="dataPassport">
      <div class="dataPassport__step">

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
            <label for="dataIssue" class="dataIssue require">Дата выдач</label>
          </div>
          <div>
            <input type="text" id="dataIssue">
          </div>
        </div>

      </div>

      <div class="dataPassport__step">

        <div class="dataPassport__step__ch">
          <div>
            <label for="series" class="series">Серия</label>
          </div>
          <div>
            <input type="number" id="series" onKeyPress="if(this.value.length===4) return false;">
          </div>
        </div>

      </div>

    </div>
  </div>
</template>

<script>
import vSelect from './select'

export default {
  name: "formClientThreeStep",
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
    }
  },
  methods: {
    optionSelect(option) {
      this.selected = option.name;
    }
  }
}
</script>

