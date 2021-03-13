<template>
  <v-container>
    <!-- <v-card class="pa-3">
      <div>
        <p></p>
      </div>
    </v-card> -->
    <v-card class="mt-6 mb-4" flat>
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
      page: 1,
      length: 0,
      lists: [],
      articleLists: [],
      pageSize: 4
    }
  },
  async asyncData ({ $content, params }) {
    const query = await $content('articles' || 'index').limit(15)
    const articles = await query.fetch()
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