<template>
    <form @submit.perevnt="handleSubmit">

        <div class="input">
            <Input v-model="firstName" :label="fnLabel" 
                :inputType="inputTypes[0]" :isRadio="false" />
            <span class="error" v-if="v$.firstName.$error">
                {{ v$.firstName.$errors[0].$message }}
            </span>
        </div>

        <div class="input">
            <Input v-model="lastName" :label="lnLabel" 
                :inputType="inputTypes[0]" :isRadio="false" />
            <span class="error" v-if="v$.lastName.$error">
                {{ v$.lastName.$errors[0].$message }}
            </span>
        </div>

        <div class="input">
            <Input v-model="dob" :label="dobLabel" 
                :inputType="inputTypes[1]" :isRadio="false" />
            <span class="error" v-if="v$.dob.$error">
                {{ v$.dob.$errors[0].$message }}
            </span>
        </div>

        <div class="input">
            <Input v-model="hcNum" :label="hcNumLabel" 
                :inputType="inputTypes[0]" :isRadio="false" />
            <span class="error" v-if="v$.hcNum.$error">
                {{ v$.hcNum.$errors[0].$message }}
            </span>
        </div>

        <div class="input">
            <Input v-model="gender" :label="genderLabel" 
                :inputType="inputTypes[2]" :isRadio="true" />
            <span class="error" v-if="v$.gender.$error">
                {{ v$.gender.$errors[0].$message }}
            </span>
        </div>

        <Button text="Submit" color="green"></Button>
    </form>
</template>

<script>
import Button from './Button'
import Input from './Input'
import useValidate from '@vuelidate/core'
import { required, numeric, alpha, minLength, maxLength, helpers }
    from '@vuelidate/validators'

const hcCheck = function(value) {
// accept only digits, dashes or spaces
    if (/[^0-9-\s]+/.test(value)) return false;

// The Luhn Algorithm
    var nCheck = 0, nDigit = 0, bEven = false;
    value = value.replace(/\D/g, "");

    for (var n = value.length - 1; n >= 0; n--) {
        var cDigit = value.charAt(n),
            nDigit = parseInt(cDigit, 10);

        if (bEven) {
            if ((nDigit *= 2) > 9) nDigit -= 9;
        }

        nCheck += nDigit;
        bEven = !bEven;
    }

    return (nCheck % 10) == 0;
}

export default {
    name: 'Form',
    components: {
        Button,
        Input
    },
    data() {
        return {
            v$: useValidate(),
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
            isRadio: false,
            isFnValid: Boolean,


        }
    },
    validations() {
        return {
            firstName: { required: helpers.withMessage('First name is required', required), alpha },
            lastName: { required: helpers.withMessage('Last name is required', required), alpha },
            dob: {
                required: helpers.withMessage('Date of birth is required', required),
                minValue: helpers.withMessage(
                    ({
                        $pending,
                        $invalid,
                        $params,
                        $model
                    }) => `The birth date is too early, you are not immortal`,
                    value => value > new Date('1900-01-01').toISOString(),
                ),


                maxValue: helpers.withMessage(
                    ({
                        $pending,
                        $invalid,
                        $params,
                        $model
                    }) => `The birth date is in the future, you are not a time lord`,
                    value => value < new Date('2022-07-06').toISOString(),
                ),
            },
            hcNum: {
                required: helpers.withMessage('Health card number is required',
                    required), numeric,
                minLength: minLength(10),
                maxLength: maxLength(10),
                hcCheck
            },
            gender: { required: helpers.withMessage('Gender is required', required) }
        }
    },
    methods: {
        handleSubmit() {
            // console.log(this.firstName, this.lastName, this.dob, this.hcNum,
            //  this.gender)
            this.v$.$validate()
            if (!this.v$.$error) {
                this.$emit("formSubmitted", [`${this.firstName} ${this.lastName}`,
                this.dob, this.hcNum, this.gender])
            } else {
                // console.log(this.v$.firstName.$errors[0].$message)

                // this.fnMsg = this.v$.firstName.$errors[0].$message

            }
        }
    }
}
</script>

<style>
    .error {
        color: red;
        font-size: smaller;
    }
</style>