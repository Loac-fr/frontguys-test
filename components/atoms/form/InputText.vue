<template>
  <div class="relative w-full">
    <input
      :id="inputId"
      ref="inputText"
      v-model="modelValue"
      :autocomplete="autocomplete"
      class="w-full p-3 lg:p-3.5 font-sans text-base lg:text-sm rounded appearance-none ring-1 ring-inset text-ellipsis whitespace-nowrap focus:outline-none disabled:text-gray-darker disabled:bg-gray disabled:cursor-not-allowed read-only:text-gray-darker read-only:bg-gray read-only:cursor-not-allowed placeholder:text-gray-darker placeholder:text-sm"
      :class="{
        'ring-gray focus:ring-gray-darker': !error,
        'ring-red focus:ring-red': error,
      }"
      :disabled="isDisabled"
      :name="inputName"
      :placeholder="placeholder"
      :readonly="isReadonly"
      :required="isRequired"
      :type="type"
    >
      <p
        v-if="error"
        class="text-xs text-red"
      >
        {{ error }}
      </p>
  </div>
</template>

<script lang="ts">
import Vue, { PropType } from 'vue';

export default Vue.extend({
  name: 'InputText',
  props: {
    autocomplete: {
      type: String,
      default: 'off',
    },
    error: {
      type: String as PropType<string | null>,
      default: null,
    },
    inputId: {
      type: String,
      default: '',
    },
    inputName: {
      type: String,
      default: '',
    },
    isDisabled: {
      type: Boolean,
      default: false,
    },
    isReadonly: {
      type: Boolean,
      default: false,
    },
    isRequired: {
      type: Boolean,
      default: false,
    },
    placeholder: {
      type: String,
      default: '',
    },
    type: {
      type: String,
      default: 'text', // should be in enum + validator
    },
    value: {
      type: String,
      required: true,
    },
  },
  computed: {
    modelValue: {
      get(): string {
        return this.value;
      },
      set(value: string): void {
        this.$emit('update:value', value);
      },
    },
  },
});
</script>
