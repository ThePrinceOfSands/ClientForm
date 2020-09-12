<template>
  <div class="formClientTwoStep">
    <div class="main">
      Адрес
    </div>

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
            <input type="text" id="town" v-model="town">
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "formClientTwoStep",
  props: ['mainData'],
  data() {
    return {
      town: '',
    }
  },
  watch: {
    town() {
      this.mainData({
        town: this.town,
      })
    }
  }
}
</script>
