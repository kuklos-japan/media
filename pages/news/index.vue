<template>
  <v-container>
    <v-layout justify-center>
      <v-img v-bind:src="logo_cryptomoney_src" max-height="200" max-width="240"></v-img>
    </v-layout>

    <v-row class="#faf9fb" justify="center">
      <div v-for="news in this.newsLists" :key="news.slug">
        <v-col>
          <nuxt-link :to="'/news/'+ news.slug" style="text-decoration: none">
            <v-card hover class="white lighten-2 ma-6" height="400" width="240">
              <v-layout justify-center>
                <v-img v-bind:src="news.image" v-bind:max-height="160" v-bind:max-width="240"></v-img>
              </v-layout>
              <v-card-title>
                {{news.title}}
              </v-card-title>
              <v-card-subtitle>
                <div>
                  <div>{{putAbstract(news.abstract1)}}</div>
                </div>
                <div>
                  <v-icon small>mdi-clock-outline</v-icon>
                  {{news.date}}
                </div>
              </v-card-subtitle>
              <v-divider class="mx-4"></v-divider>
              <v-card-text>
                <v-chip-group active-class="accent-4 white--text" column>
                  <v-chip v-for="tag in news.tags" :key="tag" class="ma-2" color="#FEE2E9" text-color="#B34778" x-small>
                    {{tag}}
                  </v-chip>
                </v-chip-group>
              </v-card-text>
            </v-card>
          </nuxt-link>
        </v-col>
      </div>
    </v-row>
    <v-pagination v-model="page" :length="length" @input="pageChange">
    </v-pagination>
    <p></p>
  </v-container>
</template>

<script>

export default {
  head() {
    return {
      title: '記事一覧'
    }
  },
  data() {
    return{
      logo_cryptomoney_src: require("@/assets/images/logo_cryptomoney.png"),
      page: 1,
      length: 0,
      newsLists: null,
      lists: [],
      newsLists: [],
      pageSize: 4,
      width: window.innerWidth,
      height: window.innerHeight
    }
  },
  async asyncData ({ $content, params }) {
    const newsQuery = await $content('news' || 'index').sortBy('date', 'desc').limit(15)
    const news = await newsQuery.fetch()

    return { lists: news }
  },
  mounted: function(){
    this.length = Math.ceil(this.lists.length/this.pageSize);
    this.newsLists = this.lists.slice(0,this.pageSize);

    this.handleResize();
    window.addEventListener('resize', this.handleResize)
  },
  beforeDestroy: function () {
    window.removeEventListener('resize', this.handleResize)
  },
  methods:{
    pageChange( pageNumber ){
      this.newsLists = this.lists.slice(this.pageSize * (pageNumber - 1),this.pageSize * (pageNumber))
    },
    handleResize: function() {
      this.width = window.innerWidth;
      this.height = window.innerHeight;
    },
    widthCheck: function() {
      if (this.width >= 900) {
        return true
      }else{
        return false
      }
    },
    putAbstract: function(abstract) {
      const MAX_LENGTH = 20
      let modStr = ''

      if (abstract !== undefined) {
        if (abstract.length > MAX_LENGTH) {
          modStr = abstract.substr(0, MAX_LENGTH) + '...'
        }else{
          modStr = abstract
        }
        return modStr
      } else {
        return ''
      }
    }
  }
}
</script>

<style scoped>
</style>