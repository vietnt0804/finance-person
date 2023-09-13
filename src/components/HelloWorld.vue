<template>
  <div class="hello" style="text-align: -webkit-center;">
    <h2>The Money follow year for finance happiness</h2>
    <div style="text-align:left; width:30%">
      <div style="display: block;">
          Init money: <input v-model="initMoney" />
      </div>
      <div style="display: block;">
          AccelerationInvest: <input v-model="accelerationInvest"/>
      </div>
      <div style="display: block;">
          accelerationInvestGrowth: <input v-model="accelerationInvestGrowth" />
      </div>
      <div style="display: block;">
          expectProfit: <input v-model="expectProfit" />
      </div>
      <div style="display: block; margin-bottom:30px;">
          expectMoney: <input v-model="expectMoney" />
      </div>

      <button @click="calculate()">
        Caculate Money
      </button>

      <div v-for="(money, index) in moneyOfYear" :key="`money-${index}`">
        Money after {{index + 1}} year: {{money}}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      moneyOfYear: [],
      initMoney: 300,
      accelerationInvest: 120,
      expectProfit: 0.2,
      expectMoney: 6000,
      accelerationInvestGrowth: 0.1
    }
  },

  mounted() {
  },

  methods: {
    calculate(){
      this.moneyOfYear = []
      this.caculateOfMoney(this.initMoney, this.accelerationInvest, this.accelerationInvestGrowth, this.expectProfit, this.expectMoney)
    },
    caculateOfMoney(initMoney, accelerationInvest, accelerationInvestGrowth, expectProfit, expectMoney, numberOfYear = 1) {
      //initMoney: Số tiền đầu tư ban đầu
      //accelerationInvest: Gia tốc đầu tư hằng năm
      //expectProfit: Lợi nhuận kỳ vọng 1 năm
      //expectMoney: Số tiền mong muốn tự do tài chính
      //accelerationInvestGrowth: Tỷ lệ tăng gia tốc hằng năm

      initMoney = parseFloat(initMoney)
      accelerationInvestGrowth = parseFloat(accelerationInvestGrowth)
      expectProfit = parseFloat(expectProfit)
      expectMoney = parseFloat(expectMoney)
      accelerationInvest = parseFloat(accelerationInvest)

      const totalInvest = parseFloat(initMoney + accelerationInvest + (accelerationInvest * accelerationInvestGrowth))
      const R = totalInvest + (totalInvest * expectProfit)
      this.moneyOfYear.push(R)
      if(R > expectMoney) {
        return 'fine'
      } else {
        numberOfYear = numberOfYear + 1
      }
      return this.caculateOfMoney(R, accelerationInvest, accelerationInvestGrowth, expectProfit, expectMoney, numberOfYear)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
