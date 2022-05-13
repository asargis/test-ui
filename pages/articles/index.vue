<template>
  <div>
    <v-row
      v-for="(item, idx) in articles"
      :key="idx"
    >
      <v-col>
        <ArticleMini
          :item="item"
        />
      </v-col>
    </v-row>
    <v-pagination
      v-model="pagination.page"
      :length="Math.ceil(pagination.total / pagination.perPage)"
      @input="next"
    ></v-pagination>
  </div>
</template>

<script>
export default {
  name: "catalog",
  data() {
    return {
      articles: [],
      pagination: {
        page: 1,
        total: 0,
        perPage: 10,
        visible: 10
      }
    }
  },
  watch: {
    articles() {

    },
  },
  methods: {
    async getLastArticles() {
      let response = await this.$axios.get('/articles')
      this.articles = response.data.data;
      this.pagination.total = response.data.meta.total;
      this.pagination.perPage = response.data.meta.per_page;
    },

    async next(page) {
      let response = await this.$axios.get('/articles?page=' + page);
      this.articles = response.data.data;
    }
  },
  async created() {
    await this.getLastArticles();
  }
}
</script>

<style scoped>

</style>
