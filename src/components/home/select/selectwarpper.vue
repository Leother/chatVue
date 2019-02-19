<template>
  <div class="select">
    <div class="education"></div>
    <div class="money"></div>
    <div class="years"></div>
  </div>
</template>

<script>
export default {
  name: "select"
}
</script>

<style scoped>
.select {
  display: flex;
}
.select div {
  flex-grow: 1;
}
</style>
