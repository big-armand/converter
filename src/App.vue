<template>
  <div id="app">
    <h1>Converter</h1>
    <div class="">
      <div class="">
        <div v-if="baseUnit != ''">Current unit : {{baseUnit}}</div>
        <div v-else>No current unit </div>
        <input @keydown.enter="addUnit" type="text" v-model="unit">
        <button @click="addUnit" type="button" name="button">Add Unit</button>
      </div>
      <div v-if="baseUnit != ''" class="">
        <input @keydown.enter="addConversion" type="text" v-model="conversion" placeholder="name/multiplier">
        <button @click="addConversion" type="button">Add Conversion Unit</button>
      </div>
    </div>
    <div v-if="baseUnit != '' && units.length != 0" class="">
      <input @keydown.enter="calculate" type="text" name="" v-model="value">
      <span> {{baseUnit}} into </span>
      <select v-model="selected">
        <option v-for="u in units" :value="u">{{u}}</option>
      </select>
      <button @click="calculate" type="button" name="submit">Compute</button>
    </div>
   <div v-if="result" class="result">
     {{result}} {{selected}}
   </div>
   <div style="color: red;" class="">
     {{error}}
   </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      value: '',
      unit: '',
      conversion: '',
      baseUnit: '',
      units: [],
      unitsRate: [],
      selected: '',
      error: '',
      result: ''
    }
  },
  methods: {
    calculate() {
      this.result = this.value * this.unitsRate[this.units.indexOf(this.selected)]
    },
    addUnit() {
      this.baseUnit = this.unit
    },
    addConversion() {
      if (this.conversion.split('/')[1]) {
        this.error = ""
        this.units.push(this.conversion.split('/')[0])
        this.unitsRate.push(this.conversion.split('/')[1])
        this.selected = this.conversion.split('/')[0]
      } else {
        this.error = "Respect the format : name/multiplier";
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
