<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <router-view/>
  <!-- 呈現環境變數 -->
  {{ name }}
  <button type="button" class="btn btn-primary">Primary</button>
</template>

<script>
// 將環境變數匯出
export default {
  data() {
    return {
      name: process.env.VUE_APP_NAME,
    };
  },
};
</script>

<style lang="scss">
@import "bootstrap";
</style>
