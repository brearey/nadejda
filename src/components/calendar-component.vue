<template>
  <div>Hello {{ like }}</div>
  <button v-on:click="addLike">Like</button>
</template>

<script lang="ts">
export default {
  data() {
    return {
      like: 0,
    }
  },
  methods: {
    addLike() {
      this.like++
    },
  },
}
</script>
