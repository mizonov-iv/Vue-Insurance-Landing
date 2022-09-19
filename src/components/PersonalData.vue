<template>
  <div class="container">
    <div class="w-50 mx-auto mt-4">
      <div>
        <label class="form-label">Имя</label>
        <input type="text" class="form-control" @blur="v$.firstName.$touch" v-model="firstName">
        <div class="text-danger small" v-for="error of v$.firstName.$errors" :key="error.$uid">Введите имя</div>
      </div>

      <div>
        <label class="form-label">Фамилия</label>
        <input type="text" class="form-control" @blur="v$.lastName.$touch" v-model="lastName">
        <div class="text-danger small" v-for="error of v$.lastName.$errors" :key="error.$uid">Введите фамилию</div>
      </div>

      <div>
        <label class="form-label">Отчество</label>
        <input type="text" class="form-control" @blur="v$.secondName.$touch" v-model="secondName">
        <div class="text-danger small" v-for="error of v$.secondName.$errors" :key="error.$uid">Введите отчество</div>
      </div>

      <div>
        <label class="form-label">Дата рождения</label>
        <input type="date" class="form-control" @blur="v$.dateOfBirth.$touch" v-model="dateOfBirth">
        <div class="text-danger small" v-for="error of v$.dateOfBirth.$errors" :key="error.$uid">Укажите дату рождения</div>
      </div>

      <div>
        <label class="form-label">Адрес регистрации</label>
        <input type="text" class="form-control" @blur="v$.adress.$touch" v-model="adress">
        <div class="text-danger small" v-for="error of v$.adress.$errors" :key="error.$uid">Укажите адрес регистрации</div>
      </div>

      <div class="d-flex">
        <button class="btn btn-outline-dark mt-3 w-100 m-1" @click="goToPayment">Перейти к оплате</button>
        <button class="btn btn-outline-dark mt-3 w-100 m-1">Вернуться к выбору страховки</button>
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
    firstName: '',
    lastName: '',
    secondName: '',
    dateOfBirth: '',
    adress: ''
  }),
  validations () {
    return {
      firstName: { required },
      lastName: { required },
      secondName: { required },
      dateOfBirth: { required },
      adress: { required }
    }
  },
  methods: {
    goToPayment(e) {
      e.preventDefault()
      this.v$.$validate()
      if(!this.v$.$error) {
        let personalData = {
          firstName: this.firstName,
          lastName: this.lastName,
          secondName: this.secondName,
          dateOfBirth: this.dateOfBirth,
          adress: this.adress
        }
        this.$emit('goToPayment', personalData)
      }
    }
  }
}
</script>

<style scoped>

</style>