<template>
  <v-app :style="{background: $vuetify.theme.themes['light'].background}">

    <!-- header -->
    <v-container class="grey lighten-5">
      <v-card class="overflow-hidden">
        <v-app-bar
          app
          color="background"
          elevate-on-scroll
        >
          <router-link to="/" style="text-decoration: none;">
            <v-img v-bind:src="logo_cryptomoney_src" max-height="64" max-width="64"></v-img>
          </router-link>
          <router-link to="/news" style="text-decoration: none;">
            <v-btn depressed plain color="black">
              お知らせ
            </v-btn>
          </router-link>
          <router-link to="/articles" style="text-decoration: none;">
            <v-btn depressed plain color="black">
              記事一覧
            </v-btn>
          </router-link>
          <!-- <v-spacer></v-spacer>
          <v-app-bar-nav-icon @click.stop="drawer = !drawer" /> -->
        </v-app-bar>
      </v-card>
    </v-container>

    <v-navigation-drawer
      app
      right
      absolute
      temporary
      v-model="drawer"
    >
      <v-list>
        <v-list-item v-for="(item, i) in items" :key="i" :to="item.to" router exact>
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

  <!-- main -->
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>

  <!-- footer -->
  <v-footer
    dark
    padless
  >
    <v-card
      class="flex"
      flat
      tile
    >
      <v-card-title class="white">
        <v-spacer></v-spacer>
        <v-spacer></v-spacer>
        <router-link to="/">
          <v-img v-bind:src="logo_cryptomoney_src" max-height="96" max-width="96"></v-img>
        </router-link>
        <v-spacer></v-spacer>
        <v-spacer></v-spacer>
        <v-spacer></v-spacer>
        <v-spacer></v-spacer>
        <v-spacer></v-spacer>
        <v-spacer></v-spacer>
        <v-spacer></v-spacer>
        <v-spacer></v-spacer>
        <v-spacer></v-spacer>
        <v-spacer></v-spacer>
        <v-spacer></v-spacer>
        <a href="https://twitter.com/CryptoM41344897" target="_blank" rel="noopener noreferrer">
          <v-img v-bind:src="logo_twitter_src" max-height="32" max-width="32"></v-img>
        </a>
        <v-spacer></v-spacer>
        <a href="https://note.com/cryptomoney" target="_blank" rel="noopener noreferrer">
          <v-img v-bind:src="logo_note_src" max-height="64" max-width="64"></v-img>
        </a>
        <v-spacer></v-spacer>
        <a href="https://discord.gg/PY4ZC44NTA" target="_blank" rel="noopener noreferrer">
          <v-img v-bind:src="logo_discord_src" max-height="36" max-width="36"></v-img>
        </a>
        <v-spacer></v-spacer>
        <v-spacer></v-spacer>

      </v-card-title>

      <v-card-text class="py-2 white--text text-center">
        {{ new Date().getFullYear() }} — <strong>&copy; CryptoMoney</strong>
      </v-card-text>
    </v-card>
  </v-footer>

  </v-app>
</template>

<script>
export default {
  data () {
    return {
      logo_cryptomoney_src: require("@/assets/images/logo_cryptomoney.png"),
      logo_note_src: require("@/assets/images/logo_note.png"),
      logo_twitter_src: require("@/assets/images/logo_twitter.png"),
      logo_discord_src: require("@/assets/images/logo_discord.png"),
      drawer: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'トップ',
          to: '/'
        },
        {
          icon: 'mdi-newspaper-variant-outline',
          title: 'お知らせ',
          to: '/news'
        },
        {
          icon: 'mdi-book-open',
          title: '記事一覧',
          to: '/articles'
        }
      ],
      title: 'Kuklos Media',
    }
  }
}
</script>

<style scoped>
.footer-text-custom-color {
  background-color: aquamarine;
  border-color: aqua;
}
</style>