<template>
    <label v-if="!isRadio">
        {{ label }}
        <input :type="inputType" v-model="inputValue">
    </label>
    <div v-else > 
        {{ label }}
        <input :type="inputType" v-model="inputValue" id="male" value="male" checked>
        <label for="male">Male</label>
        <input :type="inputType" v-model="inputValue" id="female" value="female">
        <label for="female">Female</label>
        <input :type="inputType" v-model="inputValue" id="other" value="other">
        <label for="other">Other</label>
    </div>
</template>

<script>
export default {
    name: 'Input',
    props: {
        label: String,
        modelValue: String,
        inputType: String,
        isRadio: Boolean
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

<style></style>