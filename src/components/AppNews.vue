<template>
  <div class="card">
    <h3>{{ title }}</h3>
    <app-button @action="open">{{isNewsOpen ? 'Закрыть' : 'Открыть'}}
    </app-button>
    <app-button color="danger" @action="$emit('unmark', id)" v-if="wasRead">Отметить не прочитанной </app-button>
    <div v-if="isNewsOpen">
      <hr />
      <p>
        Lorem ipsum, dolor sit amet consectetur adipisicing elit. Molestias
        illo, praesentium reiciendis, officiis est dolorem commodi ut quos earum
        atque, delectus esse numquam voluptates inventore quisquam quo ratione
        laudantium obcaecati.
      </p>
      <app-button color="primary" @action="mark" v-if="!wasRead" >Прочесть новсть</app-button>

      <app-news-list ></app-news-list>
    </div>
  </div>
</template>
<script>
import AppButton from "./AppButton.vue";
import AppNewsList from "./AppNewsList.vue";
export default {
  //  props:['title'],
  props: {
    title: String,
    id: Number,
    isOpen: Boolean,
    wasRead: Boolean,
  },
  emits: ["open-news", "mark-news", "unmark"],
  data() {
    return {
      isNewsOpen: this.isOpen,
    };
  },
  methods: {
    open() {
      this.isNewsOpen = !this.isNewsOpen;
      if (this.isNewsOpen) {
        this.$emit("open-news", 42);
      }
    },
    mark() {
      this.isNewsOpen = false;
      this.$emit("mark-news", this.id);
    },
    unmark() {},
  },
  components: {
    AppButton,
    AppNewsList
  },
};
</script>
