<template>
    <form @submit.prevent="handleSubmit">
        <Input class="input" v-model="firstName" :label="fnLabel" />
        <Input class="input" v-model="lastName" :label="lnLabel" />
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
                fnLabel: 'First Name:',
                lnLabel: 'Last Name:'
            }
        },
        methods: {
            handleSubmit () {
                console.log(this.firstName, this.lastName)
            }
        }
    }
</script>

<style>
    .input {
        display: block;
    }
</style>