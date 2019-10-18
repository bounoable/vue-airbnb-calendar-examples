<script lang="ts">
import { createComponent, ref } from '@vue/composition-api'
import { AirbnbCalendar } from 'vue-airbnb-calendar'
import MaxMonths from '../options/MaxMonths.vue'
import ContainerWidth from '../options/ContainerWidth.vue'
import { Options } from 'vue-airbnb-calendar'

export default createComponent({
  components: { AirbnbCalendar, MaxMonths, ContainerWidth },

  setup() {
    const options = ref<Options>({
      maxMonths: 4,
    })

    return {
      options,
      containerClass: ref('6xl'),
    }
  }
})
</script>

<template>
<div>
  <div class="max-w-6xl mx-auto mb-8">
    <div class="flex -mx-4 overflow-x-auto">
      <div class="px-4">
        <MaxMonths v-model="options.maxMonths"/>
      </div>

      <div class="px-4">
        <ContainerWidth v-model="containerClass"/>
      </div>
    </div>
  </div>

  <div :class="'mx-auto max-w-' + containerClass">
    <AirbnbCalendar :options="options"/>
  </div>
</div>
</template>