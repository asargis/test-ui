<template>
  <v-card
    max-width="344"
  >
    <v-text-field
      v-model="subject"
      placeholder="Тема сообщения"
      required
    />
    <v-text-field
      v-model="body"
      placeholder="Сообщение"
      required
    />
    <v-card-actions>
      <v-btn @click="send"> Отправить</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: "Comment",
  props: {
    articleId: Number,
  },
  data() {
    return {
      subject: null,
      body: null,
    }
  },
  methods: {
    async send() {
      let response = await this.$axios.post('/articles/comment', {
        subject: this.subject,
        body: this.body,
        article_id: this.articleId
      });
    }
  },
}
</script>

<style scoped>

</style>
