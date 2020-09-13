<template name="component-name">
    <div class="multiselect"
         @click="handleClick"
         @blur="focused = false"
         tabindex="-1"
         ref="parent"
    >                                  <!--Show answer options(method - handleClick - )-->

      <div class="multiselect__selected"
           v-for="(option, i) in formattedOptions"
           :key="i"
           v-show="option.checked"
      >
        {{ option[displayProperty] }}
        <span class="multiselect__remove" @click="preventClose($event); handleOptionClick(i)"> &times;</span>
      </div>

      <div class="multiselect__options"
           v-show="focused"
           :style="{top: optionsTop}"
           @click="preventClose"
      >
        <div class="multiselect__option"
             :class="{'multiselect__option--checked': option.checked}"
             v-for="(option, i) in formattedOptions"
             :key="i"
             @click="handleOptionClick(i)"

        >
          <div class="multiselect__checkbox"></div>

          <div class="multiselect__text">
            {{ option[displayProperty]}}
          </div>

        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: "multiselect",
  data() {
    return {
      focused: false, //Show answer options(bool)
      value: [],  //array of answers
      optionsTop: '34px;',
    }
  },
  computed: {
    formattedOptions() {
      return this.options.map(option => {
        let checked = this.value.some(v => v === option[this.displayProperty])
        return {...option, checked};
      });
    }
  },
  mounted() {
    this.fixTop();
  },

  methods: {
    fixTop() {
      this.optionsTop = this.$refs.parent.clientHeight + 2 + 'px';
    },
    handleClick() {
      this.focused = !this.focused; //Show answer options
    },
    preventClose(e) {
      e.stopPropagation();
    },

    handleOptionClick(i) {
      let clickedValue = this.options[i][this.displayProperty];

      let existIndex = this.value.findIndex( v => v === clickedValue);
      let newValue = [...this.value];


      if(existIndex === -1) {
        this.value.push(clickedValue);
        newValue.push(clickedValue);
      } else {
        this.value.splice(existIndex, 1);
        newValue.splice(existIndex, 1);
      }

      this.$emit('input', newValue);

      setTimeout(this.fixTop, 100);
    }
  },

  props: {
    options: {   //The main array
      type: Array,
      default() {
        return []
      },
    },
    displayProperty: {
      type: String,
      default() {
        return 'name'
      }
    },
  },
}
</script>
