<template>
  <div class="hello">
    <h1>{{category.title}}</h1>
    <p v-html="category.body"></p>
    <div v-if="posts && posts.length">
      <mu-card v-for="post of posts">
        <mu-card-header :title="post.title" subTitle="sub title">
        </mu-card-header>
        <mu-card-media title="Image Title" subTitle="Image Sub Title">
          <img :src="post.image" />
        </mu-card-media>
        <mu-card-title :title="post.title" subTitle="Content Title"/>
        <mu-card-text v-html="post.leadParagraph">
        </mu-card-text>
        <mu-card-actions>
          <mu-flat-button :to="post.slug" label="Read more..."/>
        </mu-card-actions>
      </mu-card>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

// import Breadcrumb from './Breadcrumb'

export default {
  name: 'hello',
  // components: {
  //   breadcrumb: Breadcrumb
  // },

  data () {
    return {
      category: {},
      breadcrumb: {},
      posts: [],
      errors: []
    }
  },

  // Fire a request when the component is created.
  created () {
    axios.get(`https://api.ersnet.org/news`)
    .then(response => {
      console.log(response)
      this.posts = response.data.data
      this.category = response.data.category[0]
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

.links > li {
  display: inline-block;
  margin: 0 10px;
}

.breadcrumb > li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
