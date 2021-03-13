<template>
  <v-container>
    <!-- <v-card class="pa-3">
      <div>
        <p></p>
      </div>
    </v-card> -->
    <v-card class="mt-6 mb-4" flat>
      <v-layout row wrap>
        <v-flex xs3 v-for="news in this.newsLists" :key="news.slug">
          <nuxt-link :to="'/news/'+ news.slug" style="text-decoration: none">
            <v-card hover class="white lighten-2 ma-6" height="400" width="240">
              <!-- <v-card class="ma-6" :img="require('@/assets/images/sample_01.jpg')" height="300" width="360"> -->
              <img v-bind:src="news.image" height="150" width="240" alt="">
              <v-card-title>
                {{news.title}}
              </v-card-title>
              <v-card-subtitle>
                <v-icon small>mdi-clock-outline</v-icon>
                {{news.date}}
              </v-card-subtitle>
              <v-divider class="mx-4"></v-divider>
              <v-card-text>
                <v-chip-group active-class="accent-4 white--text" column>
                  <v-chip v-for="tag in news.tags" :key="tag" class="ma-2" color="#FEE2E9" text-color="#B34778" x-small>
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
      newsLists: [],
      pageSize: 4
    }
  },
  async asyncData ({ $content, params }) {
    const query = await $content('news' || 'index').limit(15)
    const news = await query.fetch()
    return { lists: news, news }
  },
  mounted: function(){
    this.length = Math.ceil(this.lists.length/this.pageSize);
    this.newsLists = this.lists.slice(0,this.pageSize);
  },
  methods:{
    pageChange( pageNumber ){
      this.newsLists = this.lists.slice(this.pageSize * (pageNumber - 1),this.pageSize * (pageNumber))
    }
  }
}
</script>