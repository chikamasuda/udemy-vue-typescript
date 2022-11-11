<script setup lang="ts">
import { ref, reactive, computed, watch, toRefs, onBeforeMount, onMounted, onUpdated } from 'vue'

//const itemName1 = ref<string>('Desk')
const url1 = "https://www.amazon.co.jp/dp/B09JDGYSQW/ref=ods_gw_tpr_mde9_d_quad_xpl_she?pf_rd_r=RTPMRGFFM63G36RDZH45&pf_rd_p=d32fede9-eb1b-4a29-8223-5cb05808fd72&pd_rd_r=f2068548-b8a0-4843-833a-df9f86cba482&pd_rd_w=xZ0qw&pd_rd_wg=wLq3b&ref_=pd_gw_unk"

const item1 = reactive({
  name: 'Desk',
  price: 40000
})

const buy = (itemName: string) => {
    alert('Are you sure to buy ' + itemName + '?' )
}

const clear = () => {
  item1.name = ''
  item1.price = 0
}

const budget = 50000

// const priceLabel = computed(() => {
//   if (item1.price > budget * 2) {
//     return "tooooo expensive"
//   } else if (item1.price > budget) {
//     return 'expensive...'
//   } else {
//     return item1.price + 'yen'
//   }
// })

const priceLabel = ref<string>(item1.price + 'yen')

const { price } = toRefs(item1)

watch(price, () => {
  if (price.value > budget * 2) {
    priceLabel.value = "tooooo expensive"
  } else if (price.value > budget) {
    priceLabel.value = 'expensive...'
  } else {
    priceLabel.value = price.value + 'yen'
  }
})

onBeforeMount(() => {
  console.log('before mount')
})

onMounted(() => {
  console.log('mounted')
})

onUpdated(() => {
  console.log('update')
})
</script>

<template>
  <div class="container">
    <h1>Payment</h1>
    <input v-model="item1.name">
    <input v-model="item1.price">
    <button v-on:click="clear()">Clear</button>
    <div class="payment">
      <label>{{ item1.name }}</label>
      <label>{{ item1.price }}</label>
      <a v-bind:href="url1">bought at ...</a>
      <button v-on:click="buy('itemName1')">BUY</button>
    </div>
    <div class="payment">
      <label>Chair</label>
      <label>400yen</label>
      <button @click="buy('itemName1')">BUY</button>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.payment {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 80px;
  width: 400px;
  background-color: aliceblue;
  margin-bottom: 8px;
}
label {
  font-size: 20px;
  font-weight: bold;
}
input {
  margin-bottom: 8px;
}
</style>