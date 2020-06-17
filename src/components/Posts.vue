<template>
  <div class="hello mt-3">
    <ul class="list-unstyled">
      <li v-for="post in posts" class="media m-3">
        <img class="mr-3" :src="post.data.thumbnail" alt="Generic placeholder image" />
        <div class="media-body">
          <h5 class="mt-0 mb-1">{{post.data.title}}</h5>
          <div>
            <h3 class="badge badge-pill badge-primary">{{post.data.ups}} upvotes</h3>
            <p>created {{post.data.created_utc}} ago by {{post.data.author}}</p>
            <span class="badge badge-pill badge-secondary">{{post.data.num_comments}} comments</span>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
// left off at 1:33:28
// https://www.youtube.com/watch?v=6Dg6uDL1bes&t=1904s
// need to get date formatting to work
import { parse, formatDistance } from "date-fns";

export default {
  name: "Posts",
  data() {
    return {
      posts: []
    };
  },
  mounted() {
    this.load();
  },
  methods: {
    load() {
      const url = "https://www.reddit.com/r/todayilearned/.json";
      fetch(url)
        .then(response => response.json())
        .then(result => {
          this.posts = result.data.children;
        });
    }
    /*
    formatDate(date) {
      return formatDistance(parse(date, "Pp", new Date()), new Date());
    }
    */
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
