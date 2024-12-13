<template>
  <button
    class="relative inline-flex items-center justify-center p-3.5 font-sans text-sm font-semibold rounded-sm ring-1 ring-gray ring-inset disabled:opacity-40"
    data-testid="base-button"
    :disabled="isDisabled || isLoading"
    :type="buttonType"
    @click="handleClick"
  >
    <span
      v-if="isLoading"
      aria-busy="true"
      aria-live="polite"
      class="absolute w-full h-full top-3"
    >
      Loading...
    </span>
    <span
      class="z-10 transition-opacity motion-reduce:transition-none"
      :class="{
        'opacity-0': isLoading,
        'opacity-100 delay-150': !isLoading,
      }"
    >
      <slot />
    </span>
  </button>
</template>

<script lang="ts">
import Vue, { PropType } from 'vue';

enum EButtonType {
  Button = 'button',
  Submit = 'submit',
}

type ButtonType = `${EButtonType}`;

export default Vue.extend({
  name: 'BaseButton',
  props: {
    buttonType: {
      type: String as PropType<ButtonType>,
      default: EButtonType.Button,
      validator: (value: string): boolean => {
        return Object.values(EButtonType).includes(value as EButtonType);
      },
    },
    isDisabled: {
      type: Boolean,
      default: false,
    },
    isLoading: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleClick(event: Event): void {
      this.$emit('click', event);
    },
  },
});
</script>
