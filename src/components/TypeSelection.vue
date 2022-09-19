<template>
  <div class="container">
    <div class="w-50 mx-auto mt-4">
      <label class="form-label">Выбрать тип страхования</label>
      <select class="form-select" @blur="v$.chosenType.$touch" v-model="chosenType">
        <option value=""></option>
        <option value="1">Страхование жизни</option>
        <option value="2">Страхование недвижимости</option>
      </select>
      <div class="text-danger small" v-for="error of v$.chosenType.$errors" :key="error.$uid">Выберите вид страхования</div>
      <div class="d-flex">
        <button class="btn btn-outline-dark mt-3 w-100 m-1" @click="goToPersonalData">Перейти к оформлению</button>
        <button class="btn btn-outline-dark mt-3 w-100 m-1">Вернуться к расчету</button>
      </div>
    </div>
  </div>
</template>

<script>
import useVuelidate from '@vuelidate/core'
import { required } from '@vuelidate/validators'

export default {
  setup () {
    return { v$: useVuelidate() }
  },
  data: () => ({
    chosenType: ''
  }),
  validations () {
    return {
      chosenType: { required }
    }
  },
  methods: {
    goToPersonalData(e) {
      e.preventDefault()
      this.v$.$validate()
      if(!this.v$.$error) {
        let chosenType = {
          chosenType: this.chosenType
        }
        this.$emit('goToPersonalData', chosenType)
      }
    }
  }
}
</script>

<style scoped>

</style>