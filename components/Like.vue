<template>
  <div
    class="like icon"
    @click="like"
  >
    <v-icon>
      mdi-cards-heart-outline
    </v-icon>
    <div class="counter">
      <span>{{ value }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Like",
  props: {
    value: Number,
    articleId: Number,
  },
  methods: {
    async like() {
      let response = await this.$axios.post('/articles/like', {
        article_id: this.articleId
      });
      let likesCount = response.data.likes_count;
      this.$emit('like', likesCount);
    },
  },
}
</script>

<style scoped lang="sass">
.like
  &:hover
   cursor: pointer

.liked, .like > *
  margin: 0 10px 0 0

.icon
  float: right

.counter
  float: right

</style>
