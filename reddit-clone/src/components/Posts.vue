<template>
  <div class="hello mt-3">
    <h1>Posts</h1>
    <ul class="list-unstyled">
      <li v-bind:key="i" v-for="(post, i) in posts" class="media m-3">
        <img :src="post.data.thumbnail" class="mr-3" alt="Dog post" />
        <div class="media-body">
          <h5 class="mt-0 mb-1">
            <a :href="createUrl(post.data.permalink)" target="blank">{{
              post.data.title
            }}</a>
          </h5>
          <div>
            <h3 class="text-danger">{{ post.data.ups }} ⇧</h3>
            <p>
              Posted by {{ post.data.author }}
              {{ formatDate(post.data.created_utc) }}
            </p>
            <span class="badge badge-pill badge-secondary"
              >{{ post.data.num_comments }} Comments</span
            >
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import moment from 'moment';

export default {
  name: 'Posts',
  data() {
    return {
      posts: [],
    };
  },
  mounted() {
    this.load();
  },
  methods: {
    load() {
      const url = 'https://www.reddit.com/r/rarepuppers/.json';
      fetch(url)
        .then(response => response.json())
        .then(result => {
          this.posts = result.data.children;
        });
    },
    formatDate(date) {
      const created = moment.unix(date);
      const now = moment();
      return created.from(now);
    },
    createUrl(path) {
      return `https://www.reddit.com${path}`;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
