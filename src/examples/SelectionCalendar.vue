<script lang="ts">
import { createComponent, ref } from '@vue/composition-api'
import { AirbnbCalendar } from 'vue-airbnb-calendar'
import MaxMonths from '../options/MaxMonths.vue'
import ContainerWidth from '../options/ContainerWidth.vue'
import { Options, plugins } from 'vue-airbnb-calendar'
import { format } from 'date-fns'

export default createComponent({
  components: { AirbnbCalendar, MaxMonths, ContainerWidth },

  setup() {
    const options = ref<Options>({
      maxMonths: 4,
      plugins: [
        plugins.SelectionPlugin({
          colors: {
            selected: {
              background: '#bee3f8',
              border: '#63b3ed',
              text: '#2c5282',
            },
            withinSelection: {
              background: '#ebf8ff',
              border: '#90cdf4',
            },
          },

          onSelect({ from, to }) {
            if (from && to) {
              alert(format(from, 'yyyy-MM-dd') + ' - ' + format(to, 'yyyy-MM-dd'))
            }
          }
        })
      ],
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