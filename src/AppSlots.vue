<template>
  <div class="container pt-1">
    <div class="card">
      <h2>Slots</h2>
    </div>
    <app-list>
      <template #default="{index,iter}">
        <span style="color: orange">
            <strong>{{index +1}}</strong> 
            Item: {{ iter }}</span>
      </template>
    </app-list>

    <app-block>
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Eligendi,
        possimus deleniti eaque eum blanditiis, neque alias impedit hic ipsam
        harum fugit. Veniam consectetur tempore eius quaerat blanditiis, dolorum
        porro culpa.
      </p>
      <template #header>
        <h3>Its a title</h3>
      </template>
      <template #footer>
        <hr />
        <h5>Its a footer</h5>
      </template>
    </app-block>
  </div>
</template>

<script>
import AppBlock from "./components/AppBlock.vue";
import AppList from "./components/AppList.vue";
export default {
  name: "App",
  data() {
    return {
      now: new Date().toLocaleString(),
      openRate: 0,
      readRate: 0,
      news: [
        {
          title: "123",
          id: 1,
          isOpen: false,
          wasRead: false,
        },
        {
          title: "news title2",
          id: 2,
          isOpen: false,
          wasRead: false,
        },
      ],
    };
  },
  methods: {
    openNews(data) {
      this.openRate++;
      console.log(data);
    },
    markNews(id) {
      const index = this.news.findIndex((news) => news.id === id);
      this.news[index].wasRead = true;
      this.readRate++;
    },
    unmarkNews(id) {
      const news = this.news.find((news) => news.id === id);
      news.wasRead = false;
      this.readRate--;
    },
  },
  provide() {
    return {
      title: "News list",
      news: this.news,
    };
  },
  components: {
    AppBlock,
    AppList,
  },
};
</script>

<style scoped></style>
