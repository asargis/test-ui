<template>
  <v-app>
    <v-app-bar app class="top-menu">
      <v-toolbar-title>
        <NuxtLink to="/" tag="span" style="cursor: pointer">
          {{ title }}
        </NuxtLink>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-xs-only">
        <v-btn
          text
          v-for="item in items"
          :key="item.title"
          :to="item.to"
          @click="to(item)"
          class="menu-item"
          :class="{ 'active': item.active }"
        >
          <v-icon left dark>{{ item.icon }}</v-icon>
          {{ item.title }}
        </v-btn>
      </v-toolbar-items>
    </v-app-bar>

    <v-main>
      <v-container fluid>
        <Nuxt/>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {
      sidebar: false,
      items: [
        {
          title: 'На главную',
          to: '/',
          active: true,
        },
        {
          title: 'Каталог статей',
          to: '/articles',
          active: false,
        },
        {
          to: '/articles/{slug}',
        }
      ],
      title: 'Тредиум'
    }
  },
  methods: {
    to(item) {
      this.items.map(item => {
        if (item.active === true) {
          item.active = false;
        }
      });
      item.active = true;
    },
  },
  created() {
    this.items[0].active = true;
  }
}
</script>

<style scoped lang="sass">
.top-menu
  box-shadow: none !important

.menu-item.active
  border-bottom: 2px solid #6896ff

</style>
