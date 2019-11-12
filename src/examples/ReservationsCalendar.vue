<script lang="ts">
import { createComponent, ref, computed } from '@vue/composition-api'
import { AirbnbCalendar } from 'vue-airbnb-calendar'
import MaxMonths from '../options/MaxMonths.vue'
import ContainerWidth from '../options/ContainerWidth.vue'
import { Options } from 'vue-airbnb-calendar'
import SelectionPlugin from 'vue-airbnb-calendar-plugin-selection'
import { format, addMonths } from 'date-fns'
import 'vue-airbnb-calendar/dist/style.css'
import 'vue-airbnb-calendar-plugin-selection/dist/style.css'
import { Interval } from 'vue-airbnb-calendar-plugin-selection/lib/options'

export default createComponent({
  components: { AirbnbCalendar, MaxMonths, ContainerWidth },

  setup() {
    const now = new Date()

    const reservations: Interval[] = [
      {
        start: new Date(now.getFullYear(), now.getMonth(), 5),
        end: new Date(now.getFullYear(), now.getMonth(), 14),
      },
      {
        start: new Date(now.getFullYear(), now.getMonth(), 26),
        end: new Date(now.getFullYear(), now.getMonth(), 28),
      },
      {
        start: addMonths(new Date(now.getFullYear(), now.getMonth(), 14), 1),
        end: addMonths(new Date(now.getFullYear(), now.getMonth(), 25), 1),
      }
    ]

    const options = ref<Options>({
      maxMonths: 4,
      plugins: [
        SelectionPlugin({
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

          reservations: {
            ranges: reservations,
            allowCheckInOutOverlap: true,
            minDays: 7,
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