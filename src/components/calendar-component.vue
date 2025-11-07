<template>
  <div class="container">
    <div class="header">
      <button v-on:click="setPrevMonth">Previous month</button>
      <span>{{ monthsNames[currentLang][currentMonthIndex] }} {{ currentYear }}</span>
      <button v-on:click="setNextMonth">Next month</button>
      <br />
      <button v-on:click="swapLanguage">Swap language</button>
    </div>
    <div class="grid">
      <div class="week-days">
        <div class="week-day-name" v-for="weekDay in weekDaysNames[currentLang]" :key="weekDay">
          {{ weekDay }}
        </div>
      </div>
      <div class="month-days">
        <div v-for="(day, idx) in calendarDays" :key="idx">
          {{ day }}
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import {
  LANG_ENG,
  LANG_RUS,
  MONTHS_NAMES_ENG,
  MONTHS_NAMES_RUS,
  WEEK_DAYS_ENG,
  WEEK_DAYS_RUS,
} from '@/utils/constants'

export default {
  data() {
    const currentDate = new Date()
    return {
      currentLang: 'english' as 'english' | 'russian',
      currentMonthIndex: currentDate.getMonth(),
      currentYear: currentDate.getFullYear(),
      weekDaysNames: {
        english: WEEK_DAYS_ENG,
        russian: WEEK_DAYS_RUS,
      },
      monthsNames: {
        english: MONTHS_NAMES_ENG,
        russian: MONTHS_NAMES_RUS,
      },
      calendarDays: [] as number[],
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
      this.currentLang = this.currentLang === LANG_ENG ? LANG_RUS : LANG_ENG
    },
    generateCalendar() {
      const daysInMonth = new Date(this.currentYear, this.currentMonthIndex + 1, 0).getDate()
      const firstDayOfMonth = new Date(this.currentYear, this.currentMonthIndex, 1).getDay()
      const startDay = firstDayOfMonth === 0 ? 6 : firstDayOfMonth - 1
      const daysInPrevMonth = new Date(this.currentYear, this.currentMonthIndex, 0).getDate()
      const days: number[] = []

      for (let i = startDay - 1; i >= 0; i--) {
        days.push(daysInPrevMonth - i)
      }

      for (let i = 1; i <= daysInMonth; i++) {
        days.push(i)
      }

      this.calendarDays = days
    },
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
    },
  },
}
</script>

<style scoped>
.week-day-name {
  text-align: center;
}

.month-days {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 5px;
}

.week-days {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 5px;
  font-weight: bold;
  margin-bottom: 10px;
}

.month-days div {
  padding: 10px;
  text-align: center;
  border: 1px solid purple;
  border-radius: 4px;
}
</style>
