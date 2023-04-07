<template>
    <input :value="modelValue" @input="updateInput" class="input" type="text">
</template>

<script>
export default {
    name: 'my-input',
    props: {
        modelValue: [String, Number]
    },
    methods: {
        updateInput(event) {
            this.$emit('update:modelValue', event.target.value)
        }
    }
}
</script>

<style>
input {
    margin-bottom: 15px;
    width: 350px;
    height: 30px;
    border-radius: 25px;
    border: 1px solid green;
    padding: 0 10px;
}
</style>