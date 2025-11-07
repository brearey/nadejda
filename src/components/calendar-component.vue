<template>
  <div class="container">
    <div class="header">
      <button>Previous month</button>
      <span>November 2025</span>
      <button>Next month</button>
    </div>
    <div class="grid">
      <div class="week-days">
        <div v-for="weekDay in weekDays" :key="weekDay">{{ weekDay }}</div>
      </div>
      <div class="month-days">
        <div v-for="(monthDay, idx) in monthDays" :key="idx">
          {{ monthDay }}
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      weekDays: ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'],
      monthDays: [
        1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25,
        26, 27, 28, 29, 30,
      ],
    }
  },
  methods: {},
}
</script>
