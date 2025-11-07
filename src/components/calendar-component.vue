<template>
  <div class="container">
    <div class="header">
      <button>Previous month</button>
      <span>{{ monthsNames.english[currentMonthIndex] }} {{ currentYear }}</span>
      <button>Next month</button>
    </div>
    <div class="grid">
      <div class="week-days">
        <div v-for="weekDay in weekDaysNames.english" :key="weekDay">{{ weekDay }}</div>
      </div>
      <div class="month-days">
        <div v-for="(monthDay, idx) in monthDaysNumbers" :key="idx">
          {{ monthDay }}
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  data() {
    const currentDate = new Date()
    return {
      currentMonthIndex: currentDate.getMonth(),
      currentYear: currentDate.getFullYear(),
      weekDaysNames: {
        english: [
          'Monday',
          'Tuesday',
          'Wednesday',
          'Thursday',
          'Friday',
          'Saturday',
          'Sunday',
        ],
        russian: [
          'Понедельник',
          'Вторник',
          'Среда',
          'Четверг',
          'Пятница',
          'Суббота',
          'Воскресенье',
        ]
      },
      monthsNames: {
        english: [
          'January',
          'February',
          'March',
          'April',
          'May',
          'June',
          'July',
          'August',
          'September',
          'October',
          'November',
          'December',
        ],
        russian: [
          'Январь',
          'Февраль',
          'Март',
          'Апрель',
          'Май',
          'Июнь',
          'Июль',
          'Август',
          'Сентябрь',
          'Октябрь',
          'Ноябрь',
          'Декабрь',
        ],
      },
      monthDaysNumbers: [
        1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25,
        26, 27, 28, 29, 30,
      ],
    }
  },
  methods: {},
}
</script>
