<template>
  <div class="section">
    <page-title title="所得税計算" />
    <p>所得金額</p>
    <input type="number" v-model="income" placeholder="edit me" />
    <p>あなたの所得税率は{{ taxRate * 100 }}%</p>
    <p>あなたの所得税は{{ tax }}</p>
  </div>
</template>

/* 
  計算の仕組み
  https://www.nta.go.jp/taxes/shiraberu/taxanswer/shotoku/2260.htm

  給与所得控除額
  https://www.nta.go.jp/publication/pamph/koho/kurashi/html/02_1.htm
*/

<script lang="ts">
import PageTitle from "~~/components/common/PageTitle.vue";
export default {
  components: {
    "page-title": PageTitle,
  },
  data() {
    return {
      income: 0,
    }
  },
  computed: {
    tax() {
      return Math.floor(this.income * this.taxRate);
    },
    taxRate() {
      if (this.income <= 1_949_000) {
        return 0.05;
      }
      else if (this.income <= 3_299_000) {
        return 0.1;
      }
      else if (this.income <= 6_949_000) {
        return 0.20;
      }
      else if (this.income <= 8_999_000) {
        return 0.23;
      }
      else if (this.income <= 17_999_000) {
        return 0.33;
      }
      else if (this.income <= 39_999_000) {
        return 0.40;
      }
      else{
        return 0.45;
      }
    }
  }
};
</script>

<style lang="scss">

</style>
