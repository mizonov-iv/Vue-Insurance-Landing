<template>
  <div class="container">
    <form class="mt-5 w-50 mx-auto">

      <div>
        <label class="form-label">Дата рождения собственника</label>
        <input type="date" class="form-control" @blur="v$.dateOfBirth.$touch" v-model="dateOfBirth">
        <div class="text-danger small" v-for="error of v$.dateOfBirth.$errors" :key="error.$uid">Выберите дату</div>
      </div>

      <div>
        <label class="form-label">Пол</label>
        <select class="form-select" @blur="v$.gender.$touch" v-model="gender">
          <option value=""></option>
          <option value="1">мужской</option>
          <option value="2">женский</option>
        </select>
        <div class="text-danger small" v-for="error of v$.gender.$errors" :key="error.$uid">Выберите пол</div>
      </div>

      <div>
        <label class="form-label">Текущая кредитная организация</label>
        <input type="text" class="form-control" @blur="v$.currentInsuranceOrg.$touch" v-model="currentInsuranceOrg">
        <div class="text-danger small" v-for="error of v$.currentInsuranceOrg.$errors" :key="error.$uid">Введите название организации</div>
      </div>

      <div>
        <label class="form-label">Тип объекта</label>
        <select class="form-select" @blur="v$.typeOfObject.$touch" v-model="typeOfObject">
          <option value=""></option>
          <option value="1">Квартира / Апартаменты</option>
          <option value="2">Строение / Часть строения</option>
          <option value="3">Земельный участок</option>
        </select>
        <div class="text-danger small" v-for="error of v$.typeOfObject.$errors" :key="error.$uid">Выберите тип объекта</div>
      </div>

      <div>
        <label class="form-label">Введите сумму задолженности с учетом копеек</label>
        <input type="text" class="form-control" @blur="v$.debt.$touch" v-model="debt">
        <div class="text-danger small" v-for="error of v$.debt.$errors" :key="error.$uid">Введите сумму задолженности</div>
      </div>

      <button class="btn btn-outline-dark mt-3 w-100" @click="goToTypeSelection">Рассчитать</button>
    </form>
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
    dateOfBirth: '',
    gender: '',
    currentInsuranceOrg: '',
    typeOfObject: '',
    debt: ''
  }),
  validations () {
    return {
      dateOfBirth: { required },
      gender: { required },
      currentInsuranceOrg: { required },
      typeOfObject: { required },
      debt: { required }
    }
  },
  methods: {
    goToTypeSelection(e) {
      e.preventDefault()
      this.v$.$validate()
      if(!this.v$.$error) {
        let calculationResult = {
          id: Date.now(),
          dateOfBirth: this.dateOfBirth,
          gender: this.gender,
          currentInsuranceOrg: this.currentInsuranceOrg,
          typeOfObject: this.typeOfObject,
          debt: this.debt
        }
        this.$emit('goToTypeSelection', calculationResult)
      }
    }
  }

}
</script>

<style scoped>

</style>