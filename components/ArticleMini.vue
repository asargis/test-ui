<template>
  <v-card
    class="mx-auto article-mini"
    :max-width="this.mini ? 344 : 800"
  >
    <v-img
      :src="this.mini ? item.cover_mini : item.cover"
      height="300px"
    />
    <v-card-title
      class="article-link"
      @click="onTitleClick"
    >
      <v-btn
        text
        :to="'/articles/' + slug"
      >
        {{ item.title }}
      </v-btn>
    </v-card-title>

    <v-card-text class="description">
      {{ item.short_description }}
    </v-card-text>

    <v-footer>
      <Viewed :views-count="viewsCount"/>
      <v-spacer></v-spacer>
      <Like
        v-bind:value="likesCount"
        v-on:like="likesCount = $event"
        :article-id="item.id"
      />
    </v-footer>
  </v-card>
</template>

<script>
export default {
  name: "ArticleMini",
  props: {
    item: Object,
    mini: Boolean,
  },
  data() {
    return {
      liked: false,
      id: 0,
      cover: null,
      title: null,
      description: null,
      slug: null,
      likesCount: 0,
      viewsCount: 0,
      apiURL: null,
    }
  },
  methods: {
    onTitleClick(){
      console.log('on title click');
    },
  },
  watch: {
    item(newItem) {
      this.id = newItem.id;
      this.cover = this.mini ? newItem.cover_mini : newItem.cover;
      this.description = this.mini ? newItem.short_description : newItem.description;
      this.likesCount = newItem.likes_count;
      this.viewsCount = newItem.viewsCount;
      this.title = newItem.title;
      this.slug = newItem.slug;
    },
  },
  created() {
    this.id = this.item.id;
    this.cover = this.mini ? this.item.cover_mini : this.item.cover;
    this.description = this.mini ? this.item.short_description : this.description;
    this.likesCount = this.item.likes_count;
    this.viewsCount = this.item.views_count;
    this.title = this.item.title;
    this.slug = this.item.slug;

    this.apiURL = process.env.baseURL;
  }
}
</script>

<style scoped lang="sass">
.article-mini
  box-shadow: none !important

.description
  white-space: nowrap
  overflow: hidden
  padding: 5px
  text-overflow: ellipsis

.article-link
  cursor: pointer

</style>
