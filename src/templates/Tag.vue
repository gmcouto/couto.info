<template>
  <Layout>
    <h1 class="tag-title text-center space-bottom">
      # {{ $page.tag.title }}
    </h1>

    <div class="posts">
      <PostCard v-for="edge in $page.allPost.edges" :key="edge.node.id" :post="edge.node"/>
    </div>
  </Layout>
</template>

<page-query>
query Tag ($id: String!) {
  tag (id: $id) {
    title
  }
  allPost(filter: { tags: {contains: [$id]} published: { eq: true }}) {
    edges {
      node {
            title
            path
            date (format: "D. MMMM YYYY")
            timeToRead
            description
            coverImage (width: 860, blur: 10)
            content
      }
    }
  }
}
</page-query>

<script>
import Author from '~/components/Author.vue'
import PostCard from '~/components/PostCard.vue'

export default {
  components: {
    Author,
    PostCard
  },
  metaInfo () {
    return {
      title: this.$page.tag.title,
    }
  }
}
</script>

<style lang="scss">

</style>

