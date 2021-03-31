<template>

  <v-container>
    <v-layout justify-center>
      <v-img v-bind:src="logo_cryptomoney_src" max-height="200" max-width="240"></v-img>
    </v-layout>
    <p class="text-center font-weight-bold text-h3">
      いい感じの標語を入れる。
    </p>
    <v-row class="blue lighten-4" justify="center" >
      <v-col cols="12" md="12">
        <v-card color="blue" outlined tile height=150></v-card>
      </v-col>
      <v-col v-for="n in 3" :key="n" cols=12 sm=10 md=8 lg=4 xl=3>
        <v-card color="blue" outlined tile height=150></v-card>
      </v-col>
    </v-row>
    <v-card color="#faf9fb" class="mt-6 mb-4" flat>
      <v-layout row wrap>
        <v-flex xs3 v-for="article in this.articleLists" :key="article.slug">
          <nuxt-link :to="'/articles/'+ article.slug" style="text-decoration: none">
            <v-card hover class="white lighten-2 ma-6" height="400" width="240">
              <!-- <v-card class="ma-6" :img="require('@/assets/images/sample_01.jpg')" height="300" width="360"> -->
              <img v-bind:src="article.image" height="150" width="240" alt="">
              <v-card-title>
                {{article.title}}
              </v-card-title>
              <v-card-subtitle>
                <v-icon small>mdi-clock-outline</v-icon>
                {{article.date}}
              </v-card-subtitle>
              <v-divider class="mx-4"></v-divider>
              <v-card-text>
                <v-chip-group active-class="accent-4 white--text" column>
                  <v-chip v-for="tag in article.tags" :key="tag" class="ma-2" color="#FEE2E9" text-color="#B34778" x-small>
                    <!-- <v-icon left>mdi-label</v-icon> -->
                    {{tag}}
                  </v-chip>
                </v-chip-group>
              </v-card-text>
            </v-card>
          </nuxt-link>
        </v-flex>
      </v-layout>
      <v-pagination v-model="page" :length="length" @input="pageChange">
      </v-pagination>
      <p></p>
    </v-card>
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
      articleLists: [],
      pageSize: 4
    }
  },
  async asyncData ({ $content, params }) {
    const articleQuery = await $content('articles' || 'index').limit(15)
    const articles = await articleQuery.fetch()

    return { lists: articles, articles }
  },
  mounted: function(){
    this.length = Math.ceil(this.lists.length/this.pageSize);
    this.articleLists = this.lists.slice(0,this.pageSize);
  },
  methods:{
    pageChange( pageNumber ){
      this.articleLists = this.lists.slice(this.pageSize * (pageNumber - 1),this.pageSize * (pageNumber))
    }
  }
}
</script>

<style scoped>
</style>