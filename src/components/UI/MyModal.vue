<template>
    <div class="modal" v-if="show" @click="hideModal">
        <div class="modal-content" @click.stop>
            <slot></slot>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'my-modal',
        props: {
            show: {
                type: Boolean,
                required: true
            }
        },
        methods: {
            hideModal(){
                this.$emit('update:show', false);
            }
        },
    }
</script>

<style lang="scss" scoped>
    .modal{
        z-index: 999;
        width: 100%;
        height: 100%;
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: rgba(0, 0, 0, 0.4);
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .modal-content{
        background-color: white;
        border-radius: 4px;
        padding: 20px;
        border: 3px solid #4F4F4F;
    }
</style>