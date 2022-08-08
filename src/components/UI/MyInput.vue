<template>
    <input
    type="text"
    class="inp"
    :value="modelValue"
    @input="updateInput"
    >
</template>

<script>
    export default {
        name: 'my-input',
        props: {
            modelValue: [String, Number],
        },
        methods: {
            updateInput(event) {
                this.$emit('update:modelValue', event.target.value)
            }
        },
    }
</script>

<style lang="scss" scoped>
    .inp{
        border-width: 2px;
        font-weight: 400;
        font-family: inherit;
        transition: all .13s ease;
        border-radius: 4px;
        border-color: rgb(216, 229, 233);
    }
</style>