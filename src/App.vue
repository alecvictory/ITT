<template>
  <div class="container-fluid">
    <div class="row justify-content-center">
      <h1>Mortgage Calculator</h1>
    </div>
    <div class="row">
      <div class="d-flex">
        <h2>Loan Amount</h2>
        <input type="number" v-model="state.loanAmount" @input="calculateMortgage">
      </div>
      <div class="d-flex">
        <h2>Interest Rate</h2>
        <input type="number" v-model="state.loanRate" @input="calculateMortgage">
      </div>
      <div class="d-flex">
        <div class="form">
          <div class="form-group">
            <label><h5>Loan Length</h5></label>
            <select
              @input="calculateMortgage"
              v-model="state.loanLength"
              type="drop-down"
              class="form-control"
              placeholder=""
              aria-describedby="helpId"
            >
              <option>15 years</option>
              <option>30 years</option>
            </select>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="row">
    <div class="col">
      <div>
        <h2>Total Balance: ${{ state.totalBalance }}</h2>
      </div>
      <div>
        <h2>Monthly Payment: ${{ state.totalPayment }}</h2>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive } from 'vue'
export default {
  name: 'App',
  setup() {
    const state = reactive({
      loanAmount: 0,
      loanLength: 0,
      loanRate: 0,
      totalBalance: 0,
      totalPayment: 0
    })
    return {
      state,
      calculateMortgage() {
        if (!state.loanAmount || !state.loanRate || !state.loanLength) {
          state.totalBalance = 0
          state.totalPayment = 0
        };

        const r = (state.loanRate * 0.01) / 12
        const n = state.loanLength * 12
        const p = state.loanAmount

        const balance = ((r * p * n) / (1 - Math.pow(1 + r, -n))).toFixed(2)
        const pmt = (balance / n).toFixed(2)

        state.totalBalance = balance
        state.totalPayment = pmt
        console.log(state.loanAmount)
        console.log(state.loanRate)
        console.log(state.loanLength)
      }
    }
  }
}
</script>
<style lang="scss">
@import "./assets/scss/main.scss";

</style>
