<template>
    <div class="select title"
         @click="areOptionsVisible = !areOptionsVisible"
         tabindex="-1"
         ref="parent"
    >
      {{ selected }}
      <div
          class="options"
          v-if="areOptionsVisible"
          :style="{top: optionsTop}"
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
      areOptionsVisible: false,
      optionsTop: '1px;',
    }
  },

  methods: {
    selectOption(option){
      this.$emit('select', option);
      this.areOptionsVisible = false;
      setTimeout(this.fixTop, 100);
    },
    hideSelect() {
      this.areOptionsVisible = false;
    },
    fixTop() {
      this.optionsTop = this.$refs.parent.clientHeight + 1 + 'px';
    },
  },

  mounted() {
    document.addEventListener('click', this.hideSelect.bind(this), true);
    this.fixTop();
  },

  beforeDestroy() {
    document.removeEventListener('click', this.hideSelect)
  }
}

</script>
