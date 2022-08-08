<template>
    <head-item>
        <span
        @click="$emit('changeSort')"
        class="option-item"
        >
            <slot></slot>
            <my-sort-icon
            :class="[{'active': sortInfo?.active, 'reverse': sortInfo?.active && sortInfo?.reverse},'sort-icon']"
            />
        </span>
    </head-item>
</template>

<script>
    import HeadItem from '@/components/HeadItem'

    export default {
        components: { HeadItem },
        props: {
            sortInfo: {
                type: Object,
            }
        }
    }
</script>

<style lang="scss" scoped>
    .option-item{
        cursor: pointer;
        display: inline-flex;
        align-items: center;
        .sort-icon{
            opacity: 0;
            fill: #4F4F4F;
            transition: transform .14s linear, opacity .1s ease;
            &.active{
                opacity: 1;
                &.reverse{
                    transform: rotate(180deg);
                }
            }
        }
        &:hover .sort-icon:not(.active){
            opacity: .3;
        }
    }
</style>