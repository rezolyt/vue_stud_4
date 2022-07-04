<template>
  <div class="container pt-1">
    <div class="card">
      <h2>Актуальные новости c {{ now }}</h2>
      <span>Открыто: {{openRate}} | <strong>прочтиано {{readRate}} </strong></span>
    </div>
    <app-news
      v-for="item in news"
      :key="item.id"
      :title="item.title"
      :id="item.id"
      :is-open="item.isOpen"
      :was-read="item.wasRead"
      @open-news="openNews"
      @mark-news="markNews"
      @unmark="unmarkNews"
    ></app-news>
  </div>
</template>

<script>
import AppNews from "./components/AppNews.vue";

export default {
  name: "App",
  data() {
    return {
      now: new Date().toLocaleString(),
      openRate:0,
      readRate:0,
      news: [
        {
          title: "123",
          id: 1,
          isOpen: false,
          wasRead:false,
        },
        {
          title: "news title2",
          id: 2,
          isOpen: false,
          wasRead:false,
        },
      ],
    };
  },
  methods: {
    openNews(data){
      this.openRate++;
      console.log(data);
    },
    markNews(id) {
      const index = this.news.findIndex(news => news.id === id);
      this.news[index].wasRead = true;
      this.readRate++;
    },
     unmarkNews(id) {
      const news = this.news.find(news => news.id === id);
      news.wasRead = false;
      this.readRate--;
    }
  },
  provide(){
    return{
      title:'News list',
      news:this.news
    }
    
  },
  components: {
    "app-news": AppNews,
  },
};
</script>

<style scoped>
h2 {
  color:darkcyan;
}
</style>
