<template>
  <div class="vSelect">
    <div class="select">
      <p class="title"
         @click="areOptionsVisible = !areOptionsVisible"
      >
        {{ selected }}</p>
      <div
          class="options"
          v-if="areOptionsVisible"
      >
        <p
            v-for="option in options"
            :key="option.value"
            @click="selectOption(option)"
        >
          {{option.name}}
        </p>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "vSelect",
  props: {
    options: {
      type: Array,
      default() {
        return []
      }
    },
    selected: {
      type: String,
      default() {
        return '';
      }
    }
  },
  data() {
    return {
      areOptionsVisible: false
    }
  },

  methods: {
    selectOption(option){
      this.$emit('select', option);
      this.areOptionsVisible = false;
    },
    hideSelect() {
      this.areOptionsVisible = false;
    }

  },
  mounted() {
    document.addEventListener('click', this.hideSelect.bind(this), true)
  },

  beforeDestroy() {
    document.removeEventListener('click', this.hideSelect)
  }
}

</script>

<style scoped>

.vSelect {
  position: relative;
}

.select {
  position: absolute;
  min-width: 195px;
  cursor: pointer;
}

.select p {
  margin: 0;
  padding: 10px;
  border: 1px solid #ccc;
  width: 100%;
  min-height: 34px;
}

.title{
  border: 1px solid #ccc;
  border-radius: 4px;
}

.options {
  border: solid 1px #aeaeae;
  position: absolute;
  right: 0;
  width: 100%;
  margin-top: 8px;
  box-shadow: 0 3px 3px 2px #e3e3e3;
}

.options p {
  margin-top: 2px;
}

.options p:hover {
  background: #e7e7e7;
}

.title {
  border: solid 1px #aeaeae;
}
</style>