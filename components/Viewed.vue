<template>
  <div class="viewed">
    <div class="icon">
      <v-icon>
        mdi-eye
      </v-icon>
    </div>
    <div class="counter">
      <span>{{ viewsCount }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Viewed",
  props: {
    viewsCount: 0,
  },
}
</script>

<style scoped lang="sass">
.viewed > *
  margin: 0 10px 0 0
.icon
  float: left

.counter
  float: left

</style>
