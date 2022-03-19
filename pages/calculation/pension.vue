<template>
  <div>
    <page-title title="厚生年金の計算" />
    <h2>計算のソース</h2>
    <div>
      <a
        href="https://www.nenkin.go.jp/service/kounen/hokenryo/hoshu/20150515-01.html"
        >厚生年金保険の保険料
      </a>
      <a
        href="https://www.nenkin.go.jp/service/kounen/hokenryo/ryogaku/ryogakuhyo/index.html"
        >厚生年金保険料額表
      </a>
    </div>

    <h2>今年の厚生年金支払額（予想）を計算します。</h2>

    <h3>標準報酬月額の決定</h3>
    <div>
      <strong>給料を入力</strong>
      <div>
        <p>4月分</p>
        <input type="number" v-model="salaryApril" />
      </div>
      <div>
        <p>5月分</p>
        <input type="number" v-model="salaryMay" />
      </div>
      <div>
        <p>6月分</p>
        <input type="number" v-model="salaryJune" />
      </div>
    </div>

    <h3>標準賞与額の決定</h3>
    <div>
      <p>ボーナスの入力</p>
      <input type="number" v-model="bonus" />
    </div>
    <button @click="calculation">計算する</button>
    <div v-if="result">
      <p>保険の等級: {{ rank }}</p>
      <p>{{ result }}</p>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import PageTitle from "~~/components/common/PageTitle.vue";

export default defineComponent({
  components: {
    "page-title": PageTitle,
  },
  data() {
    return {
      salaryApril: 0,
      salaryMay: 0,
      salaryJune: 0,
      bonus: 0,
      /**計算結果 */
      result: 0,
    };
  },
  methods: {
    calculation() {
      console.log(this.salaryApril + this.salaryMay + this.salaryJune);
      this.result = this.salaryApril + this.salaryMay + this.salaryJune;
    },
  },
  computed: {
    rank() {
      const average = (this.salaryApril + this.salaryMay + this.salaryJune) / 3;
      /** 各保険等級の上限金額 */
      const RANK = [
        93_000, // 1
        101_000, // 2
        107_000, // 3
        114_000, // 4
        122_000, // 5
        130_000, // 6
        138_000, // 7
        146_000, // 8
        155_000, // 9
        165_000, // 10
        175_000, // 11
        185_000, // 12
        195_000, // 13
        210_000, // 14
        230_000, // 15
        250_000, // 16
        270_000, // 17
        290_000, // 18
        310_000, // 19
        330_000, // 20
        350_000, // 21
        370_000, // 22
        395_000, // 23
        425_000, // 24
        455_000, // 25
        485_000, // 26
        515_000, // 27
        545_000, // 28
        575_000, // 29
        605_000, // 30
        635_000, // 31
      ];
      const rank = RANK.findIndex((r) => r > average);
      return rank === -1 ? 32 : rank + 1;
    },
  },
});
</script>
