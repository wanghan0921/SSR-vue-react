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
          name: "aaa",
          id: 1
        },
        {
          name: "bbb",
          id: 2
        }
      ]
    };
  }
};
</script>

<style lang="sass" scoped></style>
