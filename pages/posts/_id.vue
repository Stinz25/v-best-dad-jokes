<template>
  <div class="container">
    <article>
      <h1 class="title">{{post.title}}</h1>
      <p>{{post.content}}</p>
    </article>
    <aside>
      <h3>
        <h3>Jokes you might enjoy</h3>
        <ul>
          <li :key="related.id" v-for="related in relatedPosts">
            <nuxt-link :to="{name: 'posts-id', params: {id: related.id}}">{{related.title}}</nuxt-link>
          </li>
        </ul>
      </h3>
    </aside>
  </div>
</template>

<script>
export default {
  data() {
    return {
      id: this.$route.params.id
    };
  },
  computed: {
    post() {
      return this.$store.state.posts.all.find(post => post.id === this.id);
    },
    relatedPosts() {
      return this.$store.state.posts.all.filter(post => post.id !== this.id);
    }
  },
  head() {
    const head = {
      title: 'Posts details',
      meta: [],
    }
    if (this.post != null) {
      head.title = this.post.title
      head.meta.push({
        content: this.post.content || 'No description available.',
      })
    }
    return head
  },
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: space-between;
  line-height: 1.5;
}
article * {
  margin-bottom: 1rem;
}
aside {
  min-width: 280px;
  max-width: 280px;
  padding-left: 2rem;
}
.title {
  font-size: 2rem;
}
</style>
