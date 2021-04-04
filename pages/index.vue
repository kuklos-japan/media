<template>

  <v-container>
    <v-layout justify-center>
      <v-img v-bind:src="logo_cryptomoney_src" max-height="200" max-width="340"></v-img>
    </v-layout>
    <p class="text-center font-weight-bold text-h3 ma-6">
      What is the next profitable crypto?
    </p>

    <div v-for="(article, index) in this.articleLists" :key="article.slug">
      <v-row v-if="index === 0" class="#faf9fb" justify="center">
        <v-col >
          <nuxt-link :to="'/articles/'+ article.slug" style="text-decoration: none">
            <div v-if="widthCheck()">
              <v-layout justify-center>
                <v-card hover class="white lighten-2 ma-4" height="320" width="840">
                  <v-row>
                    <v-col cols="4">
                      <v-card-title>
                        {{article.title}}
                      </v-card-title>
                      <v-card-subtitle>
                        <div>
                          <div>{{article.abstract1}}</div>
                          <div>{{article.abstract2}}</div>
                          <div>{{article.abstract3}}</div>
                        </div>
                        <div>
                          <v-icon small>mdi-clock-outline</v-icon>
                          {{article.date}}
                        </div>
                      </v-card-subtitle>
                      <v-divider class="mx-6"></v-divider>
                      <v-card-text>
                        <v-chip-group active-class="accent-4 white--text" column>
                          <v-chip v-for="tag in article.tags" :key="tag" class="ma-2" color="#FEE2E9" text-color="#B34778" x-small>
                            {{tag}}
                          </v-chip>
                        </v-chip-group>
                      </v-card-text>
                    </v-col>
                    <v-col cols="8">
                      <v-layout justify-center>
                        <v-img v-bind:src="article.image"></v-img>
                      </v-layout>
                    </v-col>
                  </v-row>
                </v-card>
              </v-layout>
            </div>
            <div v-else>
              <v-layout justify-center>
                <v-card hover class="white lighten-2 ma-6" height="400" width="240">
                  <v-layout justify-center>
                    <v-img v-bind:src="article.image" v-bind:max-height="160" v-bind:max-width="240"></v-img>
                  </v-layout>
                  <v-card-title>
                    {{article.title}}
                  </v-card-title>
                  <v-card-subtitle>
                    <div>
                      <div>{{putAbstract(article.abstract1)}}</div>
                    </div>
                    <div>
                      <v-icon small>mdi-clock-outline</v-icon>
                      {{article.date}}
                    </div>
                  </v-card-subtitle>
                  <v-divider class="mx-4"></v-divider>
                  <v-card-text>
                    <v-chip-group active-class="accent-4 white--text" column>
                      <v-chip v-for="tag in article.tags" :key="tag" class="ma-2" color="#FEE2E9" text-color="#B34778" x-small>
                        {{tag}}
                      </v-chip>
                    </v-chip-group>
                  </v-card-text>
                </v-card>
              </v-layout>
            </div>
          </nuxt-link>
        </v-col>
      </v-row>
    </div>
      <v-row class="#faf9fb" justify="center">
        <div v-for="(article, index) in this.articleLists" :key="article.slug">
          <v-col v-if="index > 0">
            <nuxt-link :to="'/articles/'+ article.slug" style="text-decoration: none">
              <v-card hover class="white lighten-2 ma-6" height="400" width="240">
                <v-layout justify-center>
                  <v-img v-bind:src="article.image" v-bind:max-height="160" v-bind:max-width="240"></v-img>
                </v-layout>
                <v-card-title>
                  {{article.title}}
                </v-card-title>
                <v-card-subtitle>
                  <div>
                    <div>{{putAbstract(article.abstract1)}}</div>
                  </div>
                  <div>
                    <v-icon small>mdi-clock-outline</v-icon>
                    {{article.date}}
                  </div>
                </v-card-subtitle>
                <v-divider class="mx-4"></v-divider>
                <v-card-text>
                  <v-chip-group active-class="accent-4 white--text" column>
                    <v-chip v-for="tag in article.tags" :key="tag" class="ma-2" color="#FEE2E9" text-color="#B34778" x-small>
                      {{tag}}
                    </v-chip>
                  </v-chip-group>
                </v-card-text>
              </v-card>
            </nuxt-link>
          </v-col>
        </div>
      </v-row>
  </v-container>
</template>

<script>
export default {
  head() {
    return {
      title: 'トップページ'
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
      pageSize: 4,
      width: window.innerWidth,
      height: window.innerHeight
    }
  },
  async asyncData ({ $content, params }) {
    const articleQuery = await $content('articles' || 'index').sortBy('date', 'desc').limit(15)
    const articles = await articleQuery.fetch()

    return { lists: articles }
  },
  mounted: function(){
    this.length = Math.ceil(this.lists.length/this.pageSize);
    this.articleLists = this.lists.slice(0,this.pageSize);

    this.handleResize();
    window.addEventListener('resize', this.handleResize)
  },
  beforeDestroy: function () {
    window.removeEventListener('resize', this.handleResize)
  },
  methods:{
    pageChange( pageNumber ){
      this.articleLists = this.lists.slice(this.pageSize * (pageNumber - 1),this.pageSize * (pageNumber))
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

      if (abstract.length > MAX_LENGTH) {
        modStr = abstract.substr(0, MAX_LENGTH) + '...'
      }else{
        modStr = abstract
      }
      return modStr
    }
  }
}
</script>

<style scoped>
</style>