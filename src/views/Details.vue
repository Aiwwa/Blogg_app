<template>
  <div v-if="error">{{ error }}</div>
  <div v-if="post" class="post">
    <h3>{{ post.title }}</h3>
    <p class="pre">{{ post.body }}</p>
  </div>
  <div v-else>Loading...</div>
</template>

<script>
import getPosts from '../composable/getPost'
import { useRoute } from 'vue-router'
export default {
  props: ['id'],
  setup(props) {
    const route = useRoute()
    const { post, error, load } = getPosts(route.params.id)

    load()

    console.log(props)

    return { post, error }
  },
}
</script>

<style scoped>
.tags a {
  margin-right: 10px;
}
.post {
  max-width: 1200px;
  margin: 0 auto;
}
.post p {
  color: #444;
  line-height: 1.5em;
  margin-top: 40px;
}
.pre {
  white-space: pre-wrap;
}
</style>
