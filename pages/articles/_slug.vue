<template>
  <v-container>
    <v-row>
      <v-col>
        <h2>{{ title }}</h2>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="1">
        <Like
          v-bind:value="likesCount"
          v-on:like="likesCount = $event"
          :article-id="articleId"
        />
      </v-col>
      <v-col cols="1">
        <Viewed :views-count="viewsCount" />
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-chip
          small
          v-for="(tag, idx) in tags"
          :href="tag.url"
          :key="idx"
        >
          {{ tag.label }}
        </v-chip>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <p> {{ body }} </p>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <Comment :article-id="articleId" />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "Article",
  data() {
    return {
      title: null,
      likesCount: 0,
      viewsCount: 0,
      tags: [],
      body: null,
      articleId: null,
      viewed: false,
    }
  },
  methods: {
    async getArticle(slug) {
      let response = await this.$axios.get('/articles/' + slug);
      if(response.data.length > 0) {
        let data = response.data[0];
        this.title = data.title;
        this.likesCount = data.likes_count;
        this.viewsCount = data.views_count;
        this.body = data.text;
        this.tags = data.tags;
        this.articleId = data.id;
      }
    },
    async view() {
      let response = await this.$axios.post('/articles/view', {
        article_id: this.articleId
      });
      this.viewsCount = response.data.views_count;
      this.viewed = true;
    },
  },
  created() {
    let slug = this.$route.params.slug;
    this.getArticle(slug);
  },
  mounted() {
    if (!this.viewed) {
      setTimeout(this.view, 5000);
    }
  }
}
</script>

<style scoped>

</style>
