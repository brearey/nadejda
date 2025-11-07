<template>
  <div class="container">
    <div class="header">
      <button v-on:click="setPrevMonth">Previous month</button>
      <span>{{ monthsNames[currentLang as keyof typeof monthsNames][currentMonthIndex] }} {{ currentYear }}</span>
      <button v-on:click="setNextMonth">Next month</button>
      <br>
      <button v-on:click="swapLanguage">Swap language</button>
    </div>
    <div class="grid">
      <div class="week-days">
        <div v-for="weekDay in weekDaysNames[currentLang as keyof typeof weekDaysNames]" :key="weekDay">{{ weekDay }}</div>
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
      currentLang: 'english',
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
      monthDaysNumbers: [] as number[],
    }
  },
  methods: {
    setNextMonth() {
      if (this.currentMonthIndex === 11) {
        this.currentMonthIndex = 0
        this.currentYear++
      } else {
        this.currentMonthIndex++
      }
      this.generateCalendar()
    },
    setPrevMonth() {
      if (this.currentMonthIndex === 0) {
        this.currentMonthIndex = 11
        this.currentYear--
      } else {
        this.currentMonthIndex--
      }
      this.generateCalendar()
    },
    swapLanguage() {
      if (this.currentLang === 'english') {
        this.currentLang = 'russian'
      } else {
        this.currentLang = 'english'
      }
    },
    generateCalendar() {
      const daysInMonth = new Date(this.currentYear, this.currentMonthIndex + 1, 0).getDate()
      this.monthDaysNumbers = Array.from({ length: daysInMonth }, (_, i) => i + 1)
    },
    getDaysInMonth(year: number, month: number): number {
      return new Date(year, month + 1, 0).getDate()
    }
  },
  mounted() {
    this.generateCalendar()
  },
  watch: {
    currentMonthIndex() {
      this.generateCalendar()
    },
    currentYear() {
      this.generateCalendar()
    }
  }
}
</script>