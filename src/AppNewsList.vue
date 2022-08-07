<template>
  <h4>{{ title }}</h4>
  <ul>
    <li v-for="item in news">{{ item.title }} <span v-if="item.wasRead">Прочитано!</span></li>
  </ul>
</template>

<script>
export default {
  inject: ['title', 'news']
}
</script>

<style scoped>

</style>