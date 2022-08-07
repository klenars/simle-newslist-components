<template>
  <div class="card">
    <h3>{{ title }}</h3>

    <app-button
        @action="open"
    >
      {{ isNewsOpen ? 'Закрыть' : 'Открыть' }}
    </app-button>

    <app-button
        color="danger"
        v-if="wasRead"
        @action="unRead"
    >
      Отметить не прочитанной
    </app-button>

    <div v-if="isNewsOpen">
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aliquid culpa ex illo iste iure
        laboriosam magnam molestias repudiandae soluta vitae.</p>
      <hr/>

      <app-button
          v-if="!wasRead"
          color="primary"
          @action="read"
      >
        Прочесть новость
      </app-button>

      <app-news-list></app-news-list>

    </div>
  </div>
</template>

<script>
import AppButton from "@/AppButton";
import AppNewsList from "@/AppNewsList";

export default {
  props: {
    title: {
      type: String,
      required: true
    },
    id: {
      type: Number,
      required: true
    },
    isOpen: {
      type: Boolean,
      required: false,
      default: false,
      validator(value) {
        return typeof value === 'boolean'
      },
    },
    wasRead: {
      type: Boolean,
      required: false
    }
  },
  emits: {
    'open-news': null,
    'read-news': null,
    'unread-news': null
  },
  data() {
    return {
      isNewsOpen: this.isOpen
    }
  },
  methods: {
    open() {
      this.isNewsOpen = !this.isNewsOpen
      if (this.isNewsOpen) {
        this.$emit('open-news')
      }
    },
    read() {
      this.isNewsOpen = false
      this.$emit('read-news')
    },
    unRead() {
      this.$emit('unread-news')
    }
  },
  components: {
    AppNewsList,
    AppButton
  }
}
</script>