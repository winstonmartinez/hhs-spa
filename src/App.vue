<template>
  <div class="container">
    <Header title="Patient Information Form" />
    <Form v-if="!isSubmitted" @formSubmitted="displayInfo" />
    <Display v-if="isSubmitted"
      :name="patientInfo[0]" 
      :dob="patientInfo[1]"
      :hcNum="patientInfo[2]"
      :gender="patientInfo[3]"/>
  </div>
</template>

<script>
import Header from './components/Header'
import Form from './components/Form'
import Display from './components/Display'
export default {
  name: 'App',
  components: {
    Header,
    Form,
    Display
  },
  data() {
    return {
      patientInfo: [],
      isSubmitted: false
    }
  },
  methods: {
    displayInfo(event) {

      this.patientInfo.push(...event)
      this.isSubmitted = true

    }
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: 'Poppins', sans-serif;
  }

  .container {
    max-width: 500px;
    margin: 30px auto;
    overflow: auto;
    min-height: 300px;
    border: 1px solid steelblue;
    padding: 30px;
    border-radius: 5px;
  }

  .btn {
    display: inline-block;
    background: #000;
    color: #fff;
    border: none;
    padding: 10px 20px;
    margin: 5px;
    border-radius: 5px;
    cursor: pointer;
    text-decoration: none;
    font-size: 15px;
    font-family: inherit;
  }

  .btn:focus {
    outline: none;
  }

  .btn:active {
    transform: scale(0.98);
  }

  .btn-block {
    display: block;
    width: 100%;
  }
</style>
