<template>
  <div class="newlist">
    <div class="container">
      <ul class="media-list">
        <li class="media" v-for="article in articles">
          <div class="media-left">
            <a v-bind:href="article.url" target="_blank">
              <img class="media-object" v-bind:src="article.urlToImage">
            </a>
          </div>
          <div class="media-body">
            <h4 class="media-heading">
              <a v-bind:href="article.url" target="_blank">{{ article.title }}</a>
            </h4>
            <h5><i>by {{ article.author }}</i></h5>
            <p>{{ article.description }}</p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'newslist',
  props: ['source'],
  data () {
    return {
      articles: []
    }
  },
  methods: {
    updateSource: function (source) {
      this.$http.get('https://newsapi.org/v1/articles?source=' + source + '&apiKey=2f5d0777ff7d48f98a4657d53b778c8a')
        .then(response => {
          this.articles = response.data.articles;
        });
    }
  },
  created: function () {
    this.updateSource(this.source);
  },
  watch: {
    source: function (val) {
      this.updateSource(val);
    }
  }
}
</script>

<style scoped>
  .media-object {
    width: 200px;
    padding: 10px;
  }
  .media {
    border-top: 1px solid lightgrey;
    padding-top: 20px;
  }
</style>