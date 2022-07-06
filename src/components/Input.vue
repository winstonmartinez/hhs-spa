<template>
    <label>
        {{ label }}
        <input type="text" v-model="inputValue">
    </label>
</template>

<script>
export default {
    name: 'Input',
    props: {
        label: String,
        modelValue: String
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