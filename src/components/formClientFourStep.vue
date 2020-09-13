<template>
<div class="confirmation">

    <div class="confirmation__text">
        Новый клиент успешно создан.
    </div>

    <div class="confirmation__checkMark"></div>

    <div class="buttonAndWarning">
      <div class="buttons">
        <button class="buttons__stepBack buttons__stepBack__clientFour"
                @click.prevent="nextStepBack"
        > Назад</button>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "formClientFourStep",
  props: ['backStep'],
  methods: {
    nextStepBack() {
      this.backStep({});
    }
  }
}
</script>


