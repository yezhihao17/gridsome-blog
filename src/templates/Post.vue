<template>
  <Layout>

    <!-- Page Header -->
    <!-- <header class="masthead" style="background-image: url('/img/post-bg.jpg')"> -->
    <header
      class="masthead"
      :style="{
        backgroundImage: `url(http://localhost:1337${article.cover.url})`
      }"
    >
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="post-heading">
              <h1>{{ article.title }}</h1>
              <!-- <h2 class="subheading">Problems look mighty small from 150 miles up</h2> -->
              <span class="meta">Posted by
                <a href="#">Start Bootstrap</a>
                on August 24, 2019</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Post Content -->
    <article>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto" v-html="markdown(article.content)"></div>
        </div>
      </div>
    </article>

    <hr>

  </Layout>
</template>

<page-query>
query ($id: ID!) {
  article: strapiPost (id: $id) {
    title
    content
    id
    cover {
      url
    }
  }
}
</page-query>

<script>
import MarkdownIt from 'markdown-it'
const md = new MarkdownIt()

export default {
  name: 'PostPage',
  computed: {
    article () {
      return this.$page.article
    }
  },
  methods: {
    markdown (content) {
      return md.render(content)
    }
  }
}
</script>

<style>

</style>
