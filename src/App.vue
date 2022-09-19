<template>
  <Navbar/>
  <Calculation @goToTypeSelection="goToTypeSelection" v-if="step.Calculation == true"/>
  <TypeSelection @goToPersonalData="goToPersonalData" v-if="step.TypeSelection == true"/>
  <PersonalData @goToPayment="goToPayment" v-if="step.PersonalData == true"/>
  <Payment v-if="step.Payment == true"/>

</template>

<script>

import Navbar from "@/components/Navbar";
import Calculation from "@/components/Calculation";
import TypeSelection from "@/components/TypeSelection";
import PersonalData from "@/components/PersonalData";
import Payment from "@/components/Payment";
import axios from "axios";
import Footer from "@/components/Footer";

export default {
  name: 'App',
  components: {
    Footer,
    Payment,
    PersonalData,
    TypeSelection,
    Calculation,
    Navbar
  },
  data: () => {
    return {
      step: {
        Calculation: true,
        TypeSelection: false,
        PersonalData: false,
        Payment: false
      }
    }
  },
  methods: {
    goToTypeSelection(calculationResult) {
      axios.post(`https://insurance-09-default-rtdb.europe-west1.firebasedatabase.app/res.json`, calculationResult)
          .then((response) => {
            if(response.status === 200) {
              this.step.Calculation = false
              this.step.TypeSelection = true
            }
          })
          .catch(error => {
              console.log('что-то пошло не так', error)
          })
    },
    goToPersonalData (chosenType) {
      axios.post(`https://insurance-09-default-rtdb.europe-west1.firebasedatabase.app/type.json`, chosenType)
          .then((response) => {
            if(response.status === 200) {
              this.step.Calculation = false
              this.step.TypeSelection = false
              this.step.PersonalData = true
            }
          })
          .catch(error => {
            console.log('что-то пошло не так', error)
          })
    },
    goToPayment (personalData) {
      axios.post(`https://insurance-09-default-rtdb.europe-west1.firebasedatabase.app/personaldata.json`, personalData)
          .then((response) => {
            if(response.status === 200) {
              this.step.Calculation = false
              this.step.TypeSelection = false
              this.step.PersonalData = false
              this.step.Payment = true
            }
          })
          .catch(error => {
            console.log('что-то пошло не так', error)
          })
    }
  }
}
</script>

<style>

</style>
