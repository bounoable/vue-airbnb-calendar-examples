<script lang="ts">
import { createComponent } from '@vue/composition-api'

export default createComponent({
  props: {
    value: {
      type: String,
      required: true,
    },
  } as const,
})
</script>

<template>
<div>
  <p class="mb-2 text-sm font-medium text-gray-700">Container width</p>
  <div class="flex items-center -mx-1">
    <button class="ContainerWidthBtn" :class="{
      'is-active': value === ''
    }" @click="$emit('input', '')">Full</button>

    <button class="ContainerWidthBtn" :class="{
      'is-active': value === '6xl'
    }" @click="$emit('input', '6xl')">6xl</button>

    <button class="ContainerWidthBtn" :class="{
      'is-active': value === '5xl'
    }" @click="$emit('input', '5xl')">5xl</button>

    <button class="ContainerWidthBtn" :class="{
      'is-active': value === '4xl'
    }" @click="$emit('input', '4xl')">4xl</button>

    <button class="ContainerWidthBtn" :class="{
      'is-active': value === '3xl'
    }" @click="$emit('input', '3xl')">3xl</button>

    <button class="ContainerWidthBtn" :class="{
      'is-active': value === '2xl'
    }" @click="$emit('input', '2xl')">2xl</button>

    <button class="ContainerWidthBtn" :class="{
      'is-active': value === 'xl'
    }" @click="$emit('input', 'xl')">xl</button>

    <button class="ContainerWidthBtn" :class="{
      'is-active': value === 'lg'
    }" @click="$emit('input', 'lg')">lg</button>

    <button class="ContainerWidthBtn" :class="{
      'is-active': value === 'md'
    }" @click="$emit('input', 'md')">md</button>

    <button class="ContainerWidthBtn" :class="{
      'is-active': value === 'sm'
    }" @click="$emit('input', 'sm')">sm</button>
  </div>
</div>
</template>

<style lang="sass" scoped>
.ContainerWidthBtn
  @apply border px-4 py-1 rounded mx-1 text-gray-700 outline-none bg-white

  @screen lg
    &:hover
      @apply bg-gray-100
  
  &.is-active
    @apply bg-gray-200 text-gray-800
</style>