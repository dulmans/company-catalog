<template>
    <button
    class="btn"
    >
        <slot></slot>
    </button>
</template>

<script>
    export default {
        name: 'my-button',
    }
</script>

<style lang="scss" scoped>
    .btn{
        cursor: pointer;
        border: 2px solid rgb(216, 229, 233);
        border-radius: 4px;
        background: none;
        font-weight: 600;
    }
</style>