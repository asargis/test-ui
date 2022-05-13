<template>
  <v-row>
    <v-col
      v-for="(item, idx) in this.articles"
      :key="idx"
      cols="12"
      sm="4"
      md="4"
      lg="4"
    >
      <ArticleMini
        :item="item"
        :mini="true"
      />
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      articles: [],
    }
  },
  methods: {
    async getLastArticles() {
      let response = await this.$axios.get('/articles/last')
      this.articles = response.data.data;
    }
  },
  async created() {
    await this.getLastArticles();
  }
}
</script>
