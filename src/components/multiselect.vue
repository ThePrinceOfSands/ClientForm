<template name="component-name">
  <div class="multiSelect">
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
  </div>
</template>




<script>
export default {
  name: "multiSelect",
  data() {
    return {
      focused: false, //Show answer options(bool)
      value: [],  //array of answers
      optionsTop: '34px;'
    }
  },
  computed: {
    formattedOptions() {
      return this.options.map(option => {
        let checked = this.value.some(v => v === option[this.valueProperty])
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
      let clickedValue = this.options[i][this.valueProperty];
      let existIndex = this.value.findIndex( v => v === clickedValue);

      if(existIndex === -1) {
        this.value.push(clickedValue);
      } else {
        this.value.splice(existIndex, 1);
      }

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
    valueProperty: {
      type: String,
      default() {
        return 'value';
      }
    },
    displayProperty: {
      type: String,
      default() {
        return 'name'
      }
    }
    }
  }
</script>

/*style for multiselect*/

<style scoped>

.multiSelect{
  position: relative;
}

.multiselect {
  background: #fff;
  padding: 6px 12px;
  border: 1px solid #ccc;
  border-radius: 4px;
  min-width: 222px;
  max-width: 226px;
  position: absolute;
  display: flex;
  flex-wrap: wrap;
  min-height: 34px;
}

.multiselect:focus {
  outline: none;
}

.multiselect__selected {
  border: 1px solid #e0e0e0;
  padding: 4px 0 4px 8px;
  margin: 3px 3px;
}

.multiselect__remove {
  cursor: pointer;
  padding-right: 7px;
}

.multiselect__remove:hover {
  color: red;
  font-weight: bold;
}

.multiselect__options {
  position: absolute;
  top: 34px;
  right: 0;
  left: 0;
  display: flex;
  background: #fff;
  flex-direction: column;
  box-shadow: 0 3px 3px 2px #e3e3e3;
  padding: 5px 0;
  min-height: 55px;
  max-height: 188px;
  overflow-y: auto;
}

.multiselect__option {
  padding: 6px 11px;
  cursor: pointer;
  display: flex;
  align-items: center;
}

.multiselect__option--checked {
  color: #1f7bb8;
  font-weight: bold;
}

.multiselect__checkbox {
  width: 22px;
  height: 22px;
  border: 1px solid #969696;
  margin-right: 7px;
  position: relative;
  /*background: #1f7bb8*/;
}

.multiselect__option--checked .multiselect__checkbox {
  border: 1px solid #1f7bb8;
  background: #1f7bb8;
}

.multiselect__option--checked .multiselect__checkbox:after {
  width: 11px;
  height: 6px;
  border-left: 2px solid rgb(255,255,255);
  border-bottom: 2px solid rgb(255,255,255);
  content: '';
  z-index: 9999;
  position: absolute;
  transform: rotate(-45deg);
  left: 3px;
  top: 4px;
}

</style>