<template>
  <div class="section">
    <p>Hello world</p>
    <page-title title="トップページ" />
    <NuxtLink to="/calculation/pension">厚生年金の計算</NuxtLink>
    <NuxtLink to="/calculation/income-tax">所得税の計算</NuxtLink>
  </div>
</template>

<script lang="ts">
import PageTitle from "~~/components/common/PageTitle.vue";
export default {
  components: {
    "page-title": PageTitle,
  },
};
</script>

<style lang="scss">
.section {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
}
</style>
