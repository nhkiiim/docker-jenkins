<template>
  <div>
    <v-sheet
      tile
      height="54"
      class="d-flex"
    >
      <v-btn
        icon
        class="ma-2"
        @click="$refs.calendar.prev()"
      >
        <v-icon>mdi-chevron-left</v-icon>
      </v-btn>
      <v-spacer></v-spacer>
      <v-btn
        icon
        class="ma-2"
        @click="$refs.calendar.next()"
      >
        <v-icon>mdi-chevron-right</v-icon>
      </v-btn>
    </v-sheet>
    <v-sheet height="600">
      <v-calendar
        ref="calendar"
        v-model="value"
        :weekdays="weekday"
        :type="type"
        :events="events"
        :event-overlap-mode="mode"
        :event-overlap-threshold="30"
        :event-color="getEventColor"
        @change="getEvents"
      ></v-calendar>
    </v-sheet>
  </div>
</template>

<script>
  export default {
    name: 'HelloWorld',
    data: () => ({
      type: 'month',
      types: ['month', 'week', 'day', '4day'],
      mode: 'stack',
      modes: ['stack', 'column'],
      weekday: [1, 2, 3, 4, 5, 6, 0],
      weekdays: [
        { text: 'Mon - Sun', value: [1, 2, 3, 4, 5, 6, 0] },
      ],
      value: '',
      events: [],
      colors: ['#FF5C4D', '#FF9636', '#FFCD58', '#DAD870'],
      names: ['김나현님 재택', '김수람님 재택', '권은님 휴가', '허예슬님 공가', '안태영님 재택', '김유민님 재택', '정소윤님 재택'],
    }),
    methods: {
      getEvents () {
        const events = []

        for (let i = 0; i < 4; i++) {
          events.push({
            name: this.names[this.rnd(0, this.names.length - 1)],
            start: new Date('2022-04-05'),
            end: new Date('2022-04-06'),
            color: this.colors[this.rnd(0, this.colors.length - 1)],
            // timed: !allDay,
          })
        }

        this.events = events
      },
      getEventColor (event) {
        return event.color
      },
      rnd (a, b) {
        return Math.floor((b - a + 1) * Math.random()) + a
      },
    },
  }
</script>