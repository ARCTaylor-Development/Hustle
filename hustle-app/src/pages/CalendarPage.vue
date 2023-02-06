<template>
    <q-page class="window-height window-width justify-center items-center">
        <div class="justify-content">
            <h2>Calendar</h2>
            <q-btn-group push>
                <q-btn push label="Previous" icon="arrow_back_ios" @click="onPrev"/>
                <q-btn push label="Today" icon="home" @click="onToday"/>
                <q-btn push label="Next" icon="arrow_forward_ios" @click="onNext"/>
            </q-btn-group>
            <div style="display: flex; max-width: 800px; width: 100%;">
                <q-calendar-month
                    ref="calendar"
                    v-model="selectedDate"
                    animated
                    bordered
                    focusable
                    hoverable
                    no-active-date
                    :day-min-height="60"
                    :day-height="0"
                    @change="onChange"
                    @moved="onMoved"
                    @click-date="onClickDate"
                    @click-day="onClickDay"
                    @click-workweek="onClickWorkweek"
                    @click-head-workweek="onClickHeadWorkweek"
                    @click-head-day="onClickHeadDay"
                    >
                    <template #week="{ scope: { week, weekdays } }">
                        <template
                        v-for="(computedEvent, index) in getWeekEvents(week, weekdays)"
                        :key="index"
                        >
                        <div
                            :class="badgeClasses(computedEvent)"
                            :style="badgeStyles(computedEvent, week.length)"
                        >
                            <div
                            v-if="computedEvent.event && computedEvent.event.details"
                            class="title q-calendar__ellipsis"
                            >
                            {{ computedEvent.event.title + (computedEvent.event.time ? ' - ' + computedEvent.event.time : '') }}
                            <q-tooltip>{{ computedEvent.event.details }}</q-tooltip>
                            </div>
                        </div>
                        </template>
                    </template>
                </q-calendar-month>
            </div>
        </div>
    </q-page>
</template>

<script>
import {
  QCalendarMonth,
  daysBetween,
  isOverlappingDates,
  parsed,
  parseDate,
  today,
  indexOf
} from '@quasar/quasar-ui-qcalendar/src/index.js'
import '@quasar/quasar-ui-qcalendar/src/QCalendarVariables.sass'
import '@quasar/quasar-ui-qcalendar/src/QCalendarTransitions.sass'
import '@quasar/quasar-ui-qcalendar/src/QCalendarMonth.sass'

import { defineComponent } from 'vue'

const CURRENT_DAY = new Date()
function getCurrentDay (day) {
  const newDay = new Date(CURRENT_DAY)
  newDay.setDate(day)
  const tm = parseDate(newDay)
  return tm.date
}

export default defineComponent({
  name: 'MonthSlotWeek',
  components: {
    QCalendarMonth
  },
  data () {
    return {
      selectedDate: today(),
      events: [
        {
          id: 1,
          title: 'Hustle Demo',
          details: 'Present demo to Mr. Bergquist',
          start: getCurrentDay(5),
          end: getCurrentDay(5),
          bgcolor: 'red'
        },
      ]
    }
  },
  methods: {
    getWeekEvents (week, weekdays) {
      const firstDay = parsed(week[ 0 ].date + ' 00:00')
      const lastDay = parsed(week[ week.length - 1 ].date + ' 23:59')

      const eventsWeek = []
      this.events.forEach((event, id) => {
        const startDate = parsed(event.start + ' 00:00')
        const endDate = parsed(event.end + ' 23:59')

        if (isOverlappingDates(startDate, endDate, firstDay, lastDay)) {
          const left = daysBetween(firstDay, startDate, true)
          const right = daysBetween(endDate, lastDay, true)

          eventsWeek.push({
            id, // index event
            left, // Position initial day [0-6]
            right, // Number days available
            size: week.length - (left + right), // Size current event (in days)
            event // Info
          })
        }
      })

      const events = []
      if (eventsWeek.length > 0) {
        const infoWeek = eventsWeek.sort((a, b) => a.left - b.left)
        infoWeek.forEach((_, i) => {
          this.insertEvent(events, week.length, infoWeek, i, 0, 0)
        })
      }

      return events
    },

    insertEvent (events, weekLength, infoWeek, index, availableDays, level) {
      const iEvent = infoWeek[ index ]
      if (iEvent !== undefined && iEvent.left >= availableDays) {
        // If you have space available, more events are placed
        if (iEvent.left - availableDays) {
          // It is filled with empty events
          events.push({ size: iEvent.left - availableDays })
        }
        // The event is built
        events.push({ size: iEvent.size, event: iEvent.event })

        if (level !== 0) {
          // If it goes into recursion, then the item is deleted
          infoWeek.splice(index, 1)
        }

        const currentAvailableDays = iEvent.left + iEvent.size

        if (currentAvailableDays < weekLength) {
          const indexNextEvent = indexOf(infoWeek, e => e.id !== iEvent.id && e.left >= currentAvailableDays)

          this.insertEvent(
            events,
            weekLength,
            infoWeek,
            indexNextEvent !== -1 ? indexNextEvent : index,
            currentAvailableDays,
            level + 1
          )
        } // else: There are no more days available, end of iteration
      }
      else {
        events.push({ size: weekLength - availableDays })
        // end of iteration
      }
    },

    badgeClasses (computedEvent) {
      if (computedEvent.event !== undefined) {
        return {
          'my-event': true,
          'text-white': true,
          [ `bg-${ computedEvent.event.bgcolor }` ]: true,
          'rounded-border': true,
          'q-calendar__ellipsis': true
        }
      }
      return {
        'my-void-event': true
      }
    },

    badgeStyles (computedEvent, weekLength) {
      const s = {}
      if (computedEvent.size !== undefined) {
        s.width = ((100 / weekLength) * computedEvent.size) + '%'
      }
      return s
    },

    isBetweenDatesWeek (dateStart, dateEnd, weekStart, weekEnd) {
      return (
        (dateEnd < weekEnd && dateEnd >= weekStart)
          || dateEnd === weekEnd
          || (dateEnd > weekEnd && dateStart <= weekEnd)
      )
    },

    onToday () {
      this.$refs.calendar.moveToToday()
    },
    onPrev () {
      this.$refs.calendar.prev()
    },
    onNext () {
      this.$refs.calendar.next()
    },
    onMoved (data) {
      console.log('onMoved', data)
    },
    onChange (data) {
      console.log('onChange', data)
    },
    onClickDate (data) {
      console.log('onClickDate', data)
    },
    onClickDay (data) {
      console.log('onClickDay', data)
    },
    onClickWorkweek (data) {
      console.log('onClickWorkweek', data)
    },
    onClickHeadDay (data) {
      console.log('onClickHeadDay', data)
    },
    onClickHeadWorkweek (data) {
      console.log('onClickHeadWorkweek', data)
    }
  }
})
</script>