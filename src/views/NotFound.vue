<template>
  <Layout>
    <p>当前页面不存在，请检查网址是否正确</p>
    <P>
      <router-link to="/">返回首页</router-link>
    </P>
  </Layout>
</template>

<script lang="ts">
export default {
  name: "NotFound",
};
</script>