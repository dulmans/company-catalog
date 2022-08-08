<template>
    <div class="pagination unselectable">
        <my-arrow
        :class="[{'hidden': currentValue === 0}, 'arrow-btn prew-btn']"
        @click="$emit('update:currentValue', currentValue - 1)"
        />
        <span>Страница: <strong>{{ currentValue + 1 }}/{{ maxPage + 1 }}</strong></span>
        <my-arrow
        :class="[{'hidden': currentValue === maxPage}, 'arrow-btn next-btn']"
        @click="$emit('update:currentValue', currentValue + 1)"
        />
    </div>
</template>

<script>
    export default {
        props: {
            currentValue: {
                type: Number,
                required: true
            },
            maxPage: {
                type: Number,
                required: true
            }
        }
    }
</script>

<style lang="scss" scoped>
    .pagination{
        display: flex;
        justify-content: flex-end;
    }

    span{
        font-weight: 400;
        font-size: 18px;
        strong{
            font-weight: 600;
        }
    }

    .arrow-btn{
        flex-basis: 18px;
        margin: 0 10px;
        cursor: pointer;
        &.hidden{
            opacity: 0;
            pointer-events: none;
        }
        &.prew-btn{
            transform: rotate(-90deg);
        }
        &.next-btn{
            transform: rotate(90deg);
        }
    }
</style>