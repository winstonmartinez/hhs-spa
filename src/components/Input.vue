<template>
    <label class="label" v-if="!isRadio">
        {{ label }}
        <input :type="inputType" v-model="inputValue">
        <span class="error" v-if="isValid">{{ fnMsg }}</span>
    </label>
    <div class="label" v-else>
        {{ label }}

        <div >
            <span class="radio-inputs">
                <input  :type="inputType"
                    v-model="inputValue" 
                    id="male" value="male">

                <label for="male">Male</label>
            </span>

            <span class="radio-inputs">
                <input class="radio-inputs" 
                    :type="inputType" 
                    v-model="inputValue" 
                    id="female" value="female">
                <label for="female">Female</label>
            </span>

            <span class="radio-inputs">
                <input class="radio-inputs" 
                    :type="inputType" 
                    v-model="inputValue" 
                    id="other" 
                    value="other">
                <label for="other">Other</label>
            </span>

            
        </div>

    </div>
</template>

<script>
export default {
    name: 'Input',
    props: {
        label: String,
        modelValue: String,
        inputType: String,
        isRadio: Boolean,
        fnMsg: String,
        isValid: Boolean
    },
    computed: {

        inputValue: {
            get() {
                return this.modelValue
            },
            set(value) {
                this.$emit('update:modelValue', value)
            }
        }
    }
}
</script>

<style>
.label {
    display: flex;
    justify-content: space-between;
    margin: 5px;
}

.radio-inputs {
    margin: 2px;
}
</style>