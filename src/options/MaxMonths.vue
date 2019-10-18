<script lang="ts">
import { createComponent } from '@vue/composition-api'

export default createComponent({
  props: {
    value: {
      type: Number,
      required: true,
    },
  } as const,

  setup(props, { emit }) {
    const down = () => {
      if (props.value <= 1) {
        return
      }

      emit('input', props.value - 1)
    }

    const up = () => emit('input', props.value + 1)

    return { down, up }
  }
})
</script>

<template>
<div>
  <p class="mb-2 text-sm font-medium text-gray-700">Max visible months</p>
  <div class="flex items-center">
    <button class="MaxMonthsBtn" @click="down">-</button>
    <span class="mx-4 text-gray-700" v-text="value"></span>
    <button class="MaxMonthsBtn" @click="up">+</button>
  </div>
</div>
</template>

<style lang="sass" scoped>
.MaxMonthsBtn
  @apply border px-4 py-1 rounded text-gray-700 outline-none bg-white

  @screen lg
    &:hover
      @apply bg-gray-100
</style>