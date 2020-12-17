<template>
  <div>
    学生页面
    <el-button>test</el-button>
    <el-button>test</el-button>
    <ul>
      <li v-for="item in list" :key="item.id">
        <nuxt-link :to="'/student/' + item.id">{{ item.name }}</nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  layout: 'headerLayout',
  data() {
    return {
      list: [
          {
            name: "aaa123",
            id: 1
          },
          {
            name: "bbb3123",
            id: 2
          }
        ]
    };
  },
  head() {
    return {
      title: '11111111111',
      meta: [
        { charset: 'utf-8' },
        { name: 'viewport', content: 'width=device-width, initial-scale=1' },
        { hid: 'description', name: 'description', content: '' }
      ]
    }
  }
};
</script>

<style lang="sass" scoped></style>
