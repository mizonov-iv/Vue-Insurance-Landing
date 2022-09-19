<template>
  <div class="container">
    <div class="w-50 mx-auto mt-4" >
      <div>
        <label class="form-label">Номер карты</label>
        <input type="text" class="form-control" @blur="v$.cardNumber.$touch" v-model="cardNumber">
        <div class="text-danger small" v-for="error of v$.cardNumber.$errors" :key="error.$uid">Введите номер карты</div>
      </div>

      <div>
        <label class="form-label">Срок действия</label>
        <input type="date" class="form-control" @blur="v$.validThru.$touch" v-model="validThru">
        <div class="text-danger small" v-for="error of v$.validThru.$errors" :key="error.$uid">Введите срок действия</div>
      </div>

      <div>
        <label class="form-label">Имя держателя</label>
        <input type="text" class="form-control" @blur="v$.name.$touch" v-model="name">
        <div class="text-danger small" v-for="error of v$.name.$errors" :key="error.$uid">Введите имя</div>
      </div>

      <div>
        <label class="form-label">CVV</label>
        <input type="date" class="form-control" @blur="v$.cvv.$touch" v-model="cvv">
        <div class="text-danger small" v-for="error of v$.cvv.$errors" :key="error.$uid">Введите с обратной стороны карты</div>
      </div>

      <div class="d-flex">
        <button class="btn btn-outline-dark mt-3 w-100 m-1" @click="showMessage">Оплатить</button>
        <button class="btn btn-outline-dark mt-3 w-100 m-1">Вернуться к личным данным</button>
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
    cardNumber: '',
    validThru: '',
    name: '',
    cvv: ''
  }),
  validations () {
    return {
      cardNumber: { required },
      validThru: { required },
      name: { required },
      cvv: { required }
    }
  },
  methods: {
    goToPayment(e) {
      e.preventDefault()
      this.v$.$validate()
      if(!this.v$.$error) {
        console.log('успех')
      }
    },
    showMessage() {
      alert('На этом пока все')
    }
  }

}
</script>

<style scoped>

</style>