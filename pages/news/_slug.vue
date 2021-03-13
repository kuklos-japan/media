<template>
  <news>
    <v-container>
      <v-layout column justify-center align-center>
        <!-- <h1>{{news.title}}</h1> -->
        <!-- <dl>
          <dd>{{news.date}}</dd>
        </dl> -->
        <div><img :src="news.image" /></div>
        <!-- <div v-for="tag in news.tags" :key="tag">{{tag}}</div> -->

        <v-flex xs12 sma12 md12 style="width: 100%">
          <div class="ma-4 markdown-body">
            <nuxt-content :document="news" />
          </div>
        </v-flex>
      </v-layout>
    </v-container>

  </news>
</template>

<script>
export default {
  async asyncData ({ $content, params }) {
    const news = await $content('news', params.slug || 'index').fetch()
    return { news }
  }
}
</script>

<style>
  /* .nuxt-content h1 {
  } */

  .nuxt-content h2 {
    position: relative;
    margin: 2.8rem 0 1.6rem;
    font-size: 1.2rem;
    font-weight: bold;
    line-height: 2rem;
    letter-spacing: .05rem
  }
  .nuxt-content h2:after {
    content: \"\";
    width:100%;
    height:1px;
    position:absolute;
    bottom:0;
    left:0;
    background-color:var(--color-primary);
    opacity:.4
  }

  .nuxt-content h3 {
    position: relative;
    margin: 2.8rem 0 1.6rem;
    font-size: 1.2rem;
    font-weight: 600;
    line-height: 1.6rem;
    letter-spacing: .05rem
  }
  .nuxt-content h3:after {
    content: \"\";
    width: 100%;
    height: 1px;
    position: absolute;
    bottom: 0;
    left: 0;
    background-color: var(--color-smoke-4);
    opacity: .4
  }

  .nuxt-content h4,
  .nuxt-content h5 {
    display: none
  }

  .nuxt-content>p {
    margin: 2rem 0;
    line-height: 1.6rem;
    letter-spacing: .05rem
  }

  .nuxt-content em {
    font-weight: 700
  }

  .nuxt-content a,
  .nuxt-content a:active,
  .nuxt-content a:visited {
    color: var(--color-on-surface);
    -webkit-text-decoration: var(--color-smoke-4) dashed underline;
    text-decoration: var(--color-smoke-4) dashed underline
  }

  .nuxt-content a:hover,
  .nuxt-content blockquote {
    color: var(--color-smoke-2)
  }

  .nuxt-content blockquote {
    margin: 1.6rem 0;
    padding: .4rem 1.6rem;
    background-color: var(--color-surface-variant)
  }

  .nuxt-content blockquote p {
    margin: .4rem 0
  }

  .nuxt-content blockquote a,
  .nuxt-content blockquote a:active,
  .nuxt-content blockquote a:visited {
    color: var(--color-smoke-2)
  }

  .nuxt-content blockquote a:hover {
    color: var(--color-smoke-3)
  }

  .nuxt-content li code,
  .nuxt-content p code {
    background-color: var(--color-surface-variant)
  }

  .nuxt-content .nuxt-content-highlight {
    margin: 1.2rem 0;
    position: relative
  }

  .nuxt-content .nuxt-content-highlight .filename {
    color: var(--color-smoke-2);
    padding: 0 .4rem;
    font-size: .8rem;
    position: absolute;
    right: 0;
    bottom: 0
  }

  .nuxt-content ol,
  .nuxt-content ul {
    padding-left: 1.6rem
  }

  .nuxt-content>ol,
  .nuxt-content>ul {
    margin: 1.2rem 0
  }

  .nuxt-content li {
    line-height: 2rem
  }

  .nuxt-content img {
    display: block;
    margin: 2.4rem auto;
    -o-object-fit: contain;
    object-fit: contain;
    max-height: 480px
  }

  .nuxt-content .footnotes {
    margin: 4rem 0
  }

  .nuxt-content .footnotes hr {
    background-color: var(--color-smoke-4);
    border: none;
    height: 1px
  }

  .nuxt-content .footnotes ol {
    list-style: decimal;
    padding-left: 2rem
  }

  .nuxt-content .footnotes ol li {
    font-size: .8rem;
    line-height: 1.6rem
  }

  .nuxt-content .footnote-backref,
  .nuxt-content .footnote-ref {
    color: var(--color-smoke-2);
    text-decoration: none
  }
</style>