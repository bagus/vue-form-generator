<template>
  <input
    :id="getFieldID(schema)"
    v-model="value"
    class="form-control"
    type="text"
    :autocomplete="schema.autocomplete"
    :disabled="disabled"
    :placeholder="schema.placeholder"
    :readonly="schema.readonly"
    :name="schema.inputName"
  />
</template>

<script>
/* global $ */
import abstractField from "../abstractField";

import { defineComponent } from "vue";

export default defineComponent({
  mixins: [abstractField],

  mounted() {
    this.$nextTick(function () {
      if (window.$ && window.$.fn.mask) {
        $(this.$el).unmask().mask(this.schema.mask, this.schema.maskOptions);
      } else {
        console.warn(
          "JQuery MaskedInput library is missing. Please download from https://github.com/digitalBush/jquery.maskedinput and load the script in the HTML head section!"
        );
      }
    });
  },

  beforeUnmount() {
    if (window.$ && window.$.fn.mask) $(this.$el).unmask();
  },
});
</script>

<style lang="scss"></style>
