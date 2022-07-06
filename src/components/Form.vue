<template>
    <form @submit.prevent="handleSubmit">
        <Input class="input" 
            v-model="firstName" 
            :label="fnLabel" 
            :inputType="inputTypes[0]"
            :isRadio="false"/>
        <Input class="input" 
            v-model="lastName" 
            :label="lnLabel" 
            :inputType="inputTypes[0]"
            :isRadio="false"/>
        <Input class="input" 
            v-model="dob"
            :label="dobLabel"
            :inputType="inputTypes[1]" 
            :isRadio="false"/>
        <Input class="input" 
            v-model="hcNum" 
            :label="hcNumLabel" 
            :inputType="inputTypes[0]"
            :isRadio="false"/>
            <Input class="input" 
            v-model="gender"
            :label="genderLabel"
            :inputType="inputTypes[2]" 
            :isRadio="true" />
        
        <Button text="Next" color="green"></Button>
    </form>
</template>

<script>
    import Button from './Button'
    import Input from './Input'
    export default {
        name: 'Form',
        components: {
            Button,
            Input
        },
        data () {
            return {
                
                firstName: '',
                lastName: '',
                dob: '',
                hcNum: '',
                gender: '',
                fnLabel: 'First Name:',
                lnLabel: 'Last Name:',
                dobLabel: 'Date of Birth: ',
                hcNumLabel: 'Health Card Number: ',
                genderLabel: 'Gender: ',
                inputTypes: ['text', 'date', 'radio'],
                isRadio: false
            }
        },
        methods: {
            handleSubmit () {
                console.log(this.firstName, this.lastName, this.dob, this.hcNum, this.gender)
            }
        }
    }
</script>

<style>
    .input {
        display: block;
    }
</style>