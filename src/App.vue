<template>
  <div class="container pt-1">
    <div class="card">
      <h2>Актуальные новости {{ now }}</h2>
      <span>Открыто: {{ openRate }} | Прочитано: {{ readRate }}</span>
    </div>

    <app-news
        v-for="item in news"
        :key="item.id"
        :title="item.title"
        :id="item.id"
        :is-open="item.isOpen"
        :was-read="item.wasRead"
        @open-news="openNews"
        @read-news="readNews(item)"
        @unread-news="unReadNews(item)"
    ></app-news>
  </div>
</template>

<script>
import AppNews from "./AppNews";

export default {
  data() {
    return {
      now: new Date().toLocaleDateString(),
      openRate: 0,
      readRate: 0,
      news: [
        {
          id: 1,
          title: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Culpa, voluptatem.',
          isOpen: false,
          wasRead: false
        },
        {
          id: 2,
          title: 'Lorem ipsum dolor sit amet.',
          isOpen: false,
          wasRead: false
        },
        {
          id: 3,
          title: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolorem, error.',
          isOpen: false,
          wasRead: false
        }
      ]
    }
  },
  provide() {
    return {
      title: 'Список новостей: ',
      news: this.news
    }
  },
  methods: {
    openNews() {
      this.openRate++
    },
    readNews(item) {
      this.readRate++
      item.wasRead = true
    },
    unReadNews(item) {
      this.readRate--
      item.wasRead = false
    }
  },
  components: {
    'app-news': AppNews
  }
}
</script>

<style>

</style>
