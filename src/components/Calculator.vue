<template>
  <section class="mt-3">
    <div class="row">
      <div class="col-4">
        <input
          class="form-control"
          type="number"
          placeholder="Operand 1"
          :disabled="loading"
          v-model="operand1"
        />
      </div>
    </div>
    <div class="row">
      <div class="col-4">
        <select class="form-control" v-model="operator" :disabled="loading">
          <option value="add">Add</option>
          <option value="subtract">Subtract</option>
          <option value="multiply">Multiply</option>
          <option value="divide">Divide</option>
        </select>
      </div>
    </div>
    <div class="row">
      <div class="col-4">
        <input
          class="form-control"
          type="number"
          placeholder="Operand 2"
          :disabled="loading"
          v-model="operand2"
        />
      </div>
    </div>
    <div class="row">
      <div class="col-4">
        <button class="btn btn-success" @click="startLoading">
          Get Result
        </button>
      </div>
    </div>
    <div class="row loader" v-show="loading">
      <pulse-loader></pulse-loader>
    </div>
    <hr />
    <h2>Result: {{ result }}</h2>
  </section>
</template>

<script>
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'

export default {
  components: {
    PulseLoader,
  },
  name: 'Calculator',
  data() {
    return {
      operand1: null,
      operand2: null,
      operator: 'add',
      result: null,
      loading: false,
    }
  },
  updated() {
    if (this.loading) {
      setTimeout(() => {
        this.getResult()
      }, 2000)
    }
  },
  methods: {
    startLoading() {
      console.log(this.operand1, this.operand2)
      if (this.operand1 === null && this.operand2 === null) {
        alert('Enter both Operands')
      } else {
        this.loading = true
      }
    },
    getResult() {
      this.operand1 = parseInt(this.operand1)
      this.operand2 = parseInt(this.operand2)

      if (this.operator == 'divide') {
        if (this.operand2 == 0) {
          alert('Can not divide by 0')
        } else {
          this.result = this.operand1 / this.operand2
        }
      } else if (this.operator == 'multiply') {
        this.result = this.operand1 * this.operand2
      } else if (this.operator == 'add') {
        this.result = this.operand1 + this.operand2
      } else {
        this.result = this.operand1 - this.operand2
      }

      this.loading = false
    },
  },
}
</script>

<style scoped>
.row {
  margin-top: 1rem;
}
.loader {
  justify-content: center;
}
</style>
